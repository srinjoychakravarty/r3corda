

# 2020 Solution Engineer Internship Srinjoy Chakravarty Exercise

*Corda Solutions Engineering Team Exercise designed by the R3 team and set by Laura Hodgkins*

# 3a) Prerequisites / Setting up

We set up our environment on a fresh Ubuntu 18.04 ISO image on VirtualBox (6.1) and got everything running smoothly.

1) Install xterm
    sudo apt-get install -y xterm

2) Install Java 8 as this is the version of Java supported by Corda (they also support Kotlin)

    sudo apt install openjdk-8-jdk openjdk-8-jre

3) Set up JAVA and JRE HOME

    cat >> /etc/environment <<EOL
JAVA_HOME= /usr/lib/jvm/java-8-openjdk-amd64
JRE_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
EOL

4) Install SDKMan so you can install the specific version of Gradle (package manager for Corda) required:

    curl -s "https://get.sdkman.io" | bash

5) Set the SDKMan source

    source "$HOME/.sdkman/bin/sdkman-init.sh"

6) Install Gradle 5.4.1 as this is the version supported by Corda.

    sdk install gradle 5.4.1

# 3a) Adding to Message State

**We added in a string parameter to the message state class to be able to send arbitrary messages via Cprda transactions**

![enter image description here](https://srinjoy-resume.herokuapp.com/img/messageState.png)

# 3b) Adding to Message Flow

We add in the newly added content parameter in Message State to Message Flow as well.

![enter image description here](https://srinjoy-resume.herokuapp.com/img/messageFlow.png)

# 3c) Adding to Message Contract

We put in a validation to ensure an empty string cannot be entered as content

![enter image description here](https://srinjoy-resume.herokuapp.com/img/messageContract.png)

# Deploying Nodes

We then prepare a Corda 3 node + 1 Notary environment by deploying the nodes.

![enter image description here](https://srinjoy-resume.herokuapp.com/img/deployNodes.png)


# Running Nodes

We then run the nodes after ensuring xterm is installed (as part of prerequisites)

![enter image description here](https://srinjoy-resume.herokuapp.com/img/runNodes.png)


# 4d) Running a Corda Flow

We can then go ahead and create a flow with our extra string type content parameter ["Srinjoy R3 2020 intern!"]

![enter image description here](https://srinjoy-resume.herokuapp.com/img/startMsgFlow.png)


# 4e) Querying a Corda Flow

Here we can see Corda's transnational privacy at work. We can query and find the transaction Party A made to Party B, in the vaults (RDBs) of Party A and Party B but not a man in the middle (i.e. Party C).

![enter image description here](https://srinjoy-resume.herokuapp.com/img/partycCantSee.png)


# Validating that Content [string] is not empty

Here we can confirm by checking that our custom validation does not allow for content to be passed as an empty string.

![enter image description here](https://srinjoy-resume.herokuapp.com/img/r3.png)

*Adds an additional requirement to the contract so that 'content' variable in MessageState cannot be an empty

# 5) Final Thoughts

Corda is trying to solve the problem of privacy when it comes to B2B transactions. How does one preserve competitive secrets while also being able to conduct trustless immutable business transactions. Businesses need to be able to trust their vendors and suppliers and vice versa without having to resort to a middleman, and that is what the Corda's financial ledger allows them to do. The privacy of the IOU's (financial promises to one another) is preserved as other parties not involved in the transaction have no visibility over it. The notary is the only node with visibility to ensure all parties behave and follow validation rules.

R3 believes a solution like Corda is superior to using public chains like Ethereum with Zero-Knowledge Proofs added on, a la Ernst&Young's implementation of NightFall. With higher throughput and better scalability, since there is no mathematical and/ or hardware overhead that ZK Proofs require, it is hard to argue against such a notion.

This engineering exercise, helped me learn how an enterprise grade distributed systems is modularized and tested. 

I am curious to see what sorts of TPS Corda can reach, when running at max capacity.



