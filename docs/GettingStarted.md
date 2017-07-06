# Logging in to Isambard

Log into Isambard using SSH:

<pre>
ssh XX-USERNAME@isambard.gw4.ac.uk
</pre>

You need to place the following into ~/.ssh/config in order to traverse the bastion hosts transparently:

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

