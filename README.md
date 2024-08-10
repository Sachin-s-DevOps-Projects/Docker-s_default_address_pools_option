# Docker Networking Issue and Solution

## Introduction

Like many people, after putting together a few docker-compose projects, I hit an error when I tried to bring a project up:

> ERROR: could not find an available, non-overlapping IPv4 address pool among the defaults to assign to the network

Specifically, this happened when I had 31 bridge networks, and tried to bring up a compose project that would increase this total to 32.

Searching for the issue, I found it was fairly common, and could be resolved by expanding the range of default address pools.

Before I tell you more - Here’s the rundown on how to fix the problem.

