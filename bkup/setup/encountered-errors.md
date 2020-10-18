# Encountered Errors

[<<](../)

## Table-of-Contents

- [Git SSH Key Passphrase](#git-ssh-key-passphrase)
- [Git Server Proxy](#git-server-proxy)
- [Git SSH Connection Timed Out](#git-ssh-connection-timed-out)
- [Port was already in use](#port-was-already-in-use)

---

## git-ssh-key-passphrase

- If you don't want to reenter your passphrase every time you use your SSH key ([Github help](https://help.github.com/en/github/authenticating-to-github/working-with-ssh-key-passphrases))
  - append content to /c/Users/you/.bashrc

    ```bash
    env=~/.ssh/agent.env

    agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

    agent_start () {
        (umask 077; ssh-agent >| "$env")
        . "$env" >| /dev/null ; }

    agent_load_env

    # agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2= agent not running
    agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

    if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
        agent_start
        ssh-add
    elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
        ssh-add
    fi

    unset env
    ```

 [~](#Table-of-Contents)

---

## git-server-proxy

```console
[ERROR] Transfer failed for https://repo.spring.io/snapshot/org/springframework/cloud/spring-cloud-context/2.2.3.BUILD-SNAPSHOT/spring-cloud-context-2.2.3.BUILD-20200329.093904-44.pom: Connect to repo.spring.io:443 [repo.spring.io/xx.xxx.xx.xx] failed: Connection timed out: connect
```

### Resolution: *add settings.xml*

- Add .m2 >> [settings.xml](./settings/settings.xml) for proxy
- Use non-snapshot version of Spring

 [~](#Table-of-Contents)

---

## git-ssh-connection-timed-out

```console
ssh: connect to host github.com port 22: Connection timed out
```

### Resolution: *set sslVerify to false*

```console
git config --global http.sslVerify false

$ git config --global --list
...
http.sslverify=false
```

### Resolution: *update config*

- Update `~/.ssh/config`

```properties
Host github.com
 Hostname ssh.github.com
 Port 443
```

 [~](#Table-of-Contents)

---

## port-was-already-in-use

```console
***************************
APPLICATION FAILED TO START
***************************
Description:
Web server failed to start. Port 8001 was already in use.

Action:
Identify and stop the process that's listening on port 8001 or configure this application to listen on another port.
```

### Resolution: *terminate process*

- `via Windows`: Run cmd as admin

    ```console
    $ netstat -ano | findstr 8001
    TCP    0.0.0.0:8001           0.0.0.0:0              LISTENING       12040

    $ taskkill /PID 12040 /F
    SUCCESS: The process with PID 12040 has been terminated.
    ```

- `via Linux`:

    ```console
    $ ps -ef | grep processName
    UID     PID    PPID  TTY        STIME COMMAND
    uid     901     597 pty0     13:04:30 /usr/bin/bash

    $ kill -9 901
    ```

- Reference
  - [DZone: How to Check Which Process Is Using Port 8080 or Any Other Port (and Vice Versa) on Windows](https://dzone.com/articles/how-to-check-which-process-is-using-port-8080-or-a)
  - [tecmint: 30 Useful 'ps Command' Examples for Linux Process Monitoring](https://www.tecmint.com/ps-command-examples-for-linux-process-monitoring/)

 [~](#Table-of-Contents)

---

[<<](../)
