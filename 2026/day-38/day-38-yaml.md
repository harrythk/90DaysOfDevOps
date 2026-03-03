## Task 1: Key-Value Pairs

# Create person.yaml that describes yourself with:
name
role
experience_years
learning (a boolean)

name: Harendra
role: L3 Support Engineer
experience_years: 11
learning: true

# Verify: Run cat person.yaml — does it look clean? No tabs?
harry@NEW4090-G8:~/my-docker-project/practice-yaml$ cat person.yaml 
name: Harendra
role: L3 Support Engineer
experience_years: 11
learning: true

Looks correct to me.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 2: Lists

# Add to person.yaml:
tools — a list of 5 DevOps tools you know or are learning
hobbies — a list using the inline format [item1, item2]

name: Harendra
role: L3 Support Engineer
experience_years: 11
learning: true
tools:
  - Linux
  - Python
  - Docker
  - Github
  - Github Actions
hobbies: [cricket, coding, traveling]

# Write in your notes: What are the two ways to write a list in YAML?
Two ways to write a list in YAML:
1. Block Style
2. Inline Style

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 3: Nested Objects

# Create server.yaml that describes a server:
server with nested keys: name, ip, port
database with nested keys: host, name, credentials (nested further: user, password)

server:
  name: Application.abc.net
  ip: 10.16.12.55
  ports:
    - "443"
database:
  host: dbserver.abc.net
  name: dbserver
  credentislas:
    user: dbuser
    password: Test@123

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Multi-line Strings

# In server.yaml, add a startup_script field using:

# The | block style (preserves newlines)

server:
  name: Application.abc.net
  ip: 10.16.12.55
  ports:
    - "443"
database:
  host: dbserver.abc.net
  name: dbserver
  credentislas:
    user: dbuser
    password: Test@123
startup_script:
  script.sh: |
    #!/bin/bash
    echo "Starting app"

# The > fold style (folds into one line)

server:
  name: Application.abc.net
  ip: 10.16.12.55
  ports:
    - "443"
database:
  host: dbserver.abc.net
  name: dbserver
  credentials:
    user: dbuser
    password: Test@123
startup_script:
  script.sh: >
    #!/bin/bash
    echo "Starting app"
    && echo "Checking dependencies"

# When would you use | vs >?

| is used when you want to keep line breaks. Normally used with shell scripting in yaml.
> is used when you want to use single line.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 5: Validate Your YAML
Install yamllint or use an online validator
Validate both your YAML files
# Intentionally break the indentation — what error do you get?

server:
  name: Application.abc.net
  ip: 10.16.12.55
  ports:
    - "443"
database:
  host: dbserver.abc.net
  name: dbserver
  credentislas:
   user: dbuser
    password: Test@123
startup_script:
  script.sh: |
    #!/bin/bash echo "Starting app"

Nested mappings are not allowed in compact mappings at line 11, column 10
Implicit keys need to be on a single line at line 11, column 10


