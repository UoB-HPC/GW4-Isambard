# Logging in to Isambard

This is the preferred method.

You must place the following into ~/.ssh/config in order to traverse the bastion hosts transparently and enable SCP usage:

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

Use the <code>login-xx.isambard.gw4.ac.uk</code> hosts when accessing the system.

If you encounter password prompts when traversing the system then you can add the following into each of the above stanzas:

<pre>
ForwardAgent yes
</pre>

## Logging onto the Bastion node

<pre>ssh XX-USERNAME@isambard.gw4.ac.uk</pre>

You will land on the bastion node, you will then need to SSH from the bastion into the system, `ssh login-01` or `ssh login-02`.

The bastion node is not intended for any user activity and has very restricted resources.
