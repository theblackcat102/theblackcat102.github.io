
Recently I got my hands on a brand new orange pi. However, I found myself stuck in typing the same boring command across all sessions. Hence, I believe this serves as a good opportunity to anisible for better automation across all servers.

Simple walkthrough the steps to install anisible in master server:

First add anisible repository:

    sudo apt-add-repository ppa:ansible/ansible -y

Install anisible:

    sudo apt-get update && sudo apt-get install ansible -y

    ansible —- version

![](https://cdn-images-1.medium.com/max/2000/1*nIAnlsZBEfFGwXUIs9fE5A.png)

Create ssh key and copy it across all web-servers:

**[ Note: username must be same as login username and same across all nodes ]**

ssh-copy-id ks@[ first node local ip ]

ssh-copy-id ks@[ second node local ip ]

Then you should be able to ssh into all servers using the master ssh public key

If all commands works out well, you can start editing /etc/ansible/hosts file and create your swarm name and local ip.

    sudo vim /etc/ansible/hosts

    [web-servers]

    192.168.0.102 [ first node local ip ]

    192.168.0.100 [ second node local ip ]

**One of many possible command in ansible**

anisible -m command -a “ your-unix-command” [your-serves-group-name]

this command send the same command to all servers

**Some Command Example:**

    ansible -m ping web-servers

    ansible -m command -a “uptime” web-servers

**Result:**

![](https://cdn-images-1.medium.com/max/2000/1*BvkXqlqpkC7qauR2y6Sa2Q.png)

    ansible -m command -a “tmux new -s foo -d” web-servers

    anisible -m command -a “tmux ls” web-servers

**Result:**

![](https://cdn-images-1.medium.com/max/2000/1*lJ-BEG7QBc9hRGhapJSAgg.png)

**Here’s a great proper introduction to ansible by Jeff Geeriling**

[youtube [https://www.youtube.com/watch?v=ZNB1at8mJWY&w=560&h=315]](https://www.youtube.com/watch?v=ZNB1at8mJWY&w=560&h=315])

如果你喜歡我的文章或side projects，可以[捐贈我一杯大熱美（大杯美式咖啡）支持我。](https://www.buymeacoffee.com/theblackcat102)