# Testing Environment
## Black Box
The tester has little or no prior knowledge about the target system.
### What It Does
* Tests the target from an external perspective
* Discovers information through the testing process
* Simulates an external attacker
* Uses publicly available information and discovered information
### What It Does Not Do
* Does not start with source code
* Does not require detailed system architecture
* Does not assume internal knowledge
* Does not require access to internal documentation
### Purpose
To determine how much an external attacker can discover, access, and exploit without prior internal knowledge.
### Good At
* Simulating real-world external attacks
* Testing the external attack surface
* Finding vulnerabilities visible from outside
* Testing how much information is exposed
### Limitations
* May miss vulnerabilities that require internal knowledge or access
* Takes more time to discover the environment
* Limited visibility into internal components
---

## Grey Box
The tester has partial knowledge or limited access to the target system.
### What It Does
* Tests with some information provided by the organization
* May use limited user accounts or credentials
* Combines external and internal perspectives
* Tests functionality available to a specific user or role
### What It Does Not Do
* Does not provide complete system knowledge
* Does not assume full administrative access
* Does not expose all internal architecture to the tester
### Purpose
To simulate an attacker who has obtained some information, credentials, or limited access.
### Good At
* Testing authenticated functionality
* Testing access control
* Testing different user roles
* Finding vulnerabilities that require some prior knowledge
* Balancing realistic attack simulation and testing coverage
### Limitations
* Less realistic than a completely external attack
* Results depend on the information and access provided
* May still miss issues requiring deeper internal knowledge
---

## White Box 
The tester has extensive knowledge of the target system.
### What It Does
* Uses detailed system information
* May have source code access
* May have architecture and configuration documentation
* May have privileged credentials
* Can inspect internal components directly
### What It Does Not Do
* Does not simulate a completely uninformed external attacker
* Does not rely only on information discovered from outside
* Does not limit testing to the external attack surface
### Purpose
To achieve extensive coverage by allowing the tester to examine the internal implementation and security controls.
### Good At
* Finding complex vulnerabilities
* Reviewing source code
* Testing internal functionality
* Identifying logic flaws
* Achieving high test coverage
* Assessing security controls in depth
### Limitations
* Less representative of a real external attacker
* Requires more information and access from the organization
* Can require more preparation and coordination
