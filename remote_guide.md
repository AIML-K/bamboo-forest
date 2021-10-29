# Remote Guide
Quick setup for freshmen in AIML, Korea University. If you have any question in great details, contact me via Slack(@wheresmadog).

Contents
1. SSH Setup
2. VPN Application
3. Further Settings

## SSH Setup
SSH connects two parties - client and host - in a secure channel and plugs client into a `terminal` on the host. Both party needs some setup to use SSH.
### Host (server)
1. Open `terminal`
2. Install `openssh-server`
    ```
    sudo apt update
    sudo apt install openssh-server
    ```
    `sudo` should require password for authentication that is set upon your account creation.
3. Start `ssh` service
    ```
    sudo service ssh start
    ```
    By default, the port is set to 22. It is strongly recommended to change the port number into something else; usually a number larger than 1024. The details are below - Further Settings.

4. Check if the service is working properly
    ```
    sudo service ssh status
    ```

### Port Forwarding in Router
1. Request administartor for authority. (contact to @wheresmadog or @d-h-lee)
2. Typing "192.168.0.1" in internet browser will lead to router setting.
3. Setup port forwarding rule in the router setup by which external port leads to your host's internal port linstening to SSH service. (detailed setting varies depending on its manufacture company)

### Client (laptop or any other PC)
1. Open `terminal` or `cmd` upon your OS
2. Connect to your remote
    ```
    ssh -p {port number} {user}@{host_ip}
    ```
    - `{port number}` is the number set up in the router.
    - `{host_ip}` is the public IP of the host, not private one in LAN.

## VPN Application
VPN directly connects to a client into a LAN as if the client is physically connected to the LAN.
1. Fill the form; 보안신청서 #3 downloaded from [here](https://ic.korea.ac.kr/ic/about/service.do).
    - Fill basic info
    - Destination IP: Check out in the router setup
    - PORT: 22
    - 사용기간: 1년
    - 사용할 ID: Pick your IDs, for example, "example1" and "example2"
    - 사용목적: SSH
2. With the form signed with your signature, request your supervisor to sign the form.
3. Visit your faculty office, and request to send the form to "정보인프라부" for the use of server.
4. The VPN request should take a couple of weeks.
5. After receiving the authenciated ID and PW pair via your email, sign in to [here](vpn.korea.ac.kr)
6. Haivng VPN running, simply turn on the `terminal` and run SSH.
    ```
    ssh -p {port number} {user}@{host ip}
    ```

## Further Readings
### Tired of inserting password every time?
For user authhentication SSH requires user password every time you connect to your host. As an alternative, you can use public key setup for the authentication.
1. Create asymmetric key pair.
    ```
    ssh-keygen -t rsa
    ```
2. Copy the public key to your host.
    - Linux/Mac
        ```
        ssh-copy-id -p {port number} {user}@{host ip}
        ```
    - Windows
        ```
        type {path to public key} | ssh -p {port} {user}@{host ip} "cat >> /.ssh/authorized_keys"
        ```
        In case of Windows, the `{path to public key}` is usually `C:\Users\{user name}\.ssh`
3. Connect your host with SSH <br>
    ```
    ssh -p {port number} {user}@{host ip}
    ```
    For this time, the server won't require any password. Because you have your client's public key planted in the host.

### How to change the port number?
On the host's side, changing port number somewhat annoymous is recommended to avoid random attacks targeting default port numbers.
1. Go to the SSH server's SSH directory
    ```
    cd /etc/ssh
    ```
2. Open `sshd_config` file using any text editors with `sudo` authority
    ```
    sudo vim sshd_config
    ```
    Personally, I prefer `vim` editor, but this is not mandatory. Choose whatever you are familiar with.
3. In the file, you should change this line.
    - Before change
        ```
        #Port 22
        ```
    - After change
        ```
        Port {any number}
        ```
