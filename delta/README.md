# Logging into NCSA Delta
[Delta](https://www.ncsa.illinois.edu/research/project-highlights/delta/) is NCSA's flagship supercomputer. You should have received information from the NCSA Identity team about your account, password, and multi-factor authentication.

To log into the system, open your Terminal and use the following command, replacing `YourUserName`:
```
ssh -l YourUserName dt-login.delta.ncsa.illinois.edu
```
and follow the prompt instructions.

# Using NGC CUDA Quantum Containers
We will use CUDA Quantum through Jupyter notebooks. To start the container, after logging into Delta, run the following command:
```
/projects/bcaf/scripts/start_container.sh
```
You will be prompted to enter a four-digit code. Choose one that you like (e.g. 5714) and take note of it. After that command goes through, the tail of the message will show something like
```
    To access the server, open this file in a browser:
        file:///u/babreu/.local/share/jupyter/runtime/jpserver-1827131-open.html
    Or copy and paste one of these URLs:
        http://gpua017.delta.ncsa.illinois.edu:5714/tree?token=7dff8e5192957d613048ab52b7e421b41782ff62771f441b
        http://127.0.0.1:5714/tree?token=7dff8e5192957d613048ab52b7e421b41782ff62771f441b
[I 2023-09-27 15:38:11.068 ServerApp] Skipped non-installed server(s): bash-language-server, dockerfile-language-server-nodejs, javascript-typescript-langserver, jedi-language-server, julia-language-server, pyright, python-language-server, python-lsp-server, r-languageserver, sql-language-server, texlab, typescript-language-server, unified-language-server, vscode-css-languageserver-bin, vscode-html-languageserver-bin, vscode-json-languageserver-bin, yaml-language-server

```
The key information you need is under the `Or copy and paste one of these URLs:` line (4th line in the snippet above). You will need the name of the compute node where the container is running. In this example, the node name is `gpua017`.

With this information in hand, open another Terminal window (don't close the previous one!), and enter the following command, replacing `YouserUserName` with your username, `NodeName` with what you got in the previous step and `PortNumber` with the four-digit code you chose before.
```
ssh -l YourUserName -L 127.0.0.1:PortNumber:NodeName.delta.internal.ncsa.edu:PortNumber dt-login.delta.ncsa.illinois.edu
```
You will be prompted to authenticate on Delta again. Finally, paste the entire second URL (right below where you found the node name, starts with `http://127.0.0.1`, 5th line in the snippet above) on your local browser, and you are connected and can use notebooks now!

## Summary of steps
1. Log into Delta
```
ssh -l YourUserName dt-login.delta.ncsa.illinois.edu
```
2. Start the container and take note of the chosen port number
```
/projects/bcaf/scripts/start_container.sh
```
3. Find the node name (it will be `gpua###`)
4. With the port number and the node name, open another Terminal and tunnel through the login node:
```
ssh -l YourUserName -L 127.0.0.1:PortNumber:NodeName.delta.internal.ncsa.edu:PortNumber dt-login.delta.ncsa.illinois.edu
```
5. Copy the URL with the node name and the token (`http://127.0.0.1......`) into your local browser
