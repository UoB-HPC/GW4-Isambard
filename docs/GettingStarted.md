# Logging in to Isambard

You need to place the following into ~/.ssh/config in order to traverse the bastion hosts transparently and to enable SCP usage:

<pre>
Host isambard.gw4.ac.uk
  User XX-USERNAME

Host login-01.isambard.gw4.ac.uk
  Hostname login-01
  User XX-USERNAME
  ProxyCommand ssh isambard.gw4.ac.uk 'nc %h %p'

Host login-02.isambard.gw4.ac.uk
  Hostname login-02
  User XX-USERNAME
  ProxyCommand ssh isambard.gw4.ac.uk 'nc %h %p'
</pre>

## Logging onto the Bastion node

<pre>ssh XX-USERNAME@isambard.gw4.ac.uk</pre>

You will land on the bastion node, you will then need to SSH from the bastion into the system, `ssh login-01` or `ssh login-02`.

The bastion node is not intended for any user activity and has very restricted resources.
