---
layout: page
title: Paxos Consensus Mechanism
description: Implementing the Paxos consensus algorithm in Java for distributed consensus.
img: assets/img/paxos.png
importance: 4
category: fun
---

### Project Overview

This Java-based project implements the [Paxos consensus mechanism](https://en.wikipedia.org/wiki/Paxos_(computer_science)), providing a robust distributed algorithm for achieving consensus among a network of CouncilMembers. The system follows key Paxos algorithm phases, including connect, prepare, accept, and consensus, utilizing a central server to facilitate communication.

The Paxos algorithm provides a mechanism that enables distributed systems to continue working predictably in the event of network partitioning or server failures. As long as a client application can communicate with key roles in a distributed system, then distributed storage, for example, can function as predictably as a thread-safe data structure.

Paxos is usually used where durability is needed to replicate large datasets, such as a file or a database. The protocol attempts to make progress even during periods when some bounded number of replicas are unresponsive. Paxos also provides the ability to drop or add new replicas as components fail or become unreliable.

### Features

- **Connect Phase:** CouncilMembers establish connections to the central server.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/paxos connect.png" title="connect phase image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>


- **Prepare Phase:** Proposers send prepare messages, and Acceptors respond with promises.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/paxos promise.png" title="promise phase image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

- **Accept Phase:** Proposers send Accept_Request messages, and Acceptors accept based on previous promises.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/paxos acceptance.png" title="acceptance phase image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

- **Consensus Phase:** Achieve consensus when a proposer receives a majority of Accept messages.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/consensus.png" title="consensus phase image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

### Design Choices

- The system employs a central server for communication (Server.java).
- CouncilMembers include both Proposers (Proposer.java) and Acceptors (Acceptor.java).
- Robustness is ensured through back-off mechanisms ensuring the system comes to consensus and message delay handling.



{% if site.data.repositories.github_repos %}
<div class="text-center">
  <div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-center align-items-center">
    {% for repo in site.data.repositories.Paxos %}
      {% include repository/repo.html repository=repo %}
    {% endfor %}
  </div>
</div>
{% endif %}