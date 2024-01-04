---
layout: page
title: Paxos Consensus Mechanism
description: Implementing the Paxos consensus algorithm in Java for distributed consensus among CouncilMembers.
img:
importance: 4
category: fun
---

### Project Overview

This Java-based project implements the [Paxos consensus mechanism](https://en.wikipedia.org/wiki/Paxos_(computer_science)), providing a robust distributed algorithm for achieving consensus among a network of CouncilMembers. The system follows key Paxos algorithm phases, including connect, prepare, accept, and consensus, utilizing a central server to facilitate communication. 

### Features

- **Connect Phase:** CouncilMembers establish connections to the central server.
- **Prepare Phase:** Proposers send prepare messages, and Acceptors respond with promises.
- **Accept Phase:** Proposers send Accept_Request messages, and Acceptors accept based on previous promises.
- **Consensus Phase:** Achieve consensus when a proposer receives a majority of Accept messages.

### Design Choices

- The system employs a central server for communication (Server.java).
- CouncilMembers include both Proposers (Proposer.java) and Acceptors (Acceptor.java).
- Robustness is ensured through back-off mechanisms and message delay handling.



{% if site.data.repositories.github_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.Paxos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}