### Data Crunching on a Shoestring Budget
Ville Tuulos

    image

![image](images/big_logo.png)<br>
developer platform for real-time data<br><br>

we &hearts; scripts

    notes

## FAQ
### I want to use<br>
Riak<br>
Disco<br>
MongoDB<br>
...<br>
### How should I run it in Amazon EC2?

    notes

## <span class="upside-down">FAQ</span>
### I want to use<br>
Amazon EC2<br>
Rackspace<br>
Softlayer<br>
...<br>
### How should I build my system?

    notes

environmental pressure

    notes (doing anything else would be really expensive)

![image](images/Brontosaurus-inv.png)

    notes

![image](images/Canvasback_duck_BW-inv.png)

    notes

<h3 class="principle">
<strong>Cloud</strong><br>
Bitdeli<br>
Erlang<br>
</h3>

    notes

<div class="title">1) Many Small Short-Living Instances</div>
![image](images/cicada.png)

    notes

<h3 class="principle">1) Many small <strong>short living</strong> instances</h3>
EC2 Annual Uptime Percentage<br>
##99.95%
21.9 minutes downtime per month<br>
##Per Region

    notes

<h3 class="principle">1) Many small <strong>short living</strong> instances</h3>
![image](images/ec2pricing.svg)<br>

    notes

<h3 class="principle">1) <strong>Many small</strong> short living instances</h3>
![image](images/17gb-price.svg)<br>

    notes

<div class="title">2) Avoid Disk IO</div>
![image](images/gramophone_BW_T.png)

    notes

<h3 class="principle">2) Avoid <strong>Disk IO</strong></h3>

<h3 class="principle">Local Disk</h3>
unpredictable, requires initialization
<h3 class="principle">Elastic Block Store</h3>
unpredictable, slow
<h3 class="principle">RAID over Elastic Block Store</h3>
complex, expensive

    notes

<h3 class="principle">2) <strong>Avoid</strong> Disk IO</h3>

<pre>
Dear Ville Tuulos,

Your volume experienced a failure
due to multiple failures of the
underlying hardware components
and we were unable to recover it.
...

Sincerely,
EBS Support
</pre>

    notes

<div class="title">3) Separate Workloads</div>
![image](images/horse_drawn_cart.png)

    notes

<h3 class="principle">3) Separate <strong>Workloads</strong></h3>

<table class="workloads">
<thead>
<tr><td>Workload</td><td>Data</td><td>Latency</td><td>Req/Sec</td><td>Cost</td><td>Failing</td></tr>
</thead>
<tbody>
<tr><td>Web Frontend</td><td>&lt;100GB</td><td>&lt;100ms</td><td>1-1000+</td><td>$$</td><td>horrible</td></tr>
<tr><td>Low-Latency</td><td>&lt;1GB</td><td>&lt;500ms</td><td>1-10</td><td>$$</td><td>bad</td></tr>
<tr><td>Batch</td><td>&lt;1TB</td><td>&lt;1h</td><td>0.1-1</td><td>$$$</td><td>ok</td></tr>
<tr><td>Best Effort</td><td>&infin;</td><td>&infin;</td><td>~0</td><td>$</td><td>expected</td></tr>
</tbody>
</table>

    notes

<h3 class="principle">3) <strong>Separate</strong> Workloads</h3>

<table class="workloads">
<thead>
<tr><td>Workload</td><td>RAM</td><td>CPU</td><td># instances</td><td>Type</td></tr>
</thead>
<tbody>
<tr><td>Web Frontend</td><td>1-4GB</td><td>low</td><td>1-3</td><td>VPS / Dedicated</td></tr>
<tr><td>Low-Latency</td><td>&lt;1GB</td><td>spiky</td><td>1-100</td><td>Micro / Small</td></tr>
<tr><td>Batch</td><td>1GB+</td><td>high</td><td>1-10</td><td>Small / Medium</td></tr>
<tr><td>Best Effort</td><td>-</td><td>-</td><td></td><td>-</td></tr>
</tbody>
</table>

    notes

<h3 class="principle">3) Separate Workloads</h3>

Cheapest instance with at least 1GB RAM

<table class="workloads">
<thead>
<tr><td>Provider</td><td>Price/Month</td><td>RAM</td></tr>
</thead>
<tbody>
<tr><td>AWS</td><td>$31</td><td>1.7GB</td></tr>
<tr><td>Linode</td><td>$40</td><td>1GB</td></tr>
<tr><td>Rackspace</td><td>$44</td><td>1GB</td></tr>
<tr><td>SoftLayer</td><td>$50</td><td>1GB</td></tr>
</tbody>
</table>

    notes

<div class="title">4) Antifragility</div>
![image](images/haeckel.png)

    notes

<h3 class="principle">4) Antifragility</h3>

<pre style="font-size: 80%">
Just as a package sent by mail can bear a stamp
"fragile", "breakable" or "handle with care",
consider the exact opposite: a package that has
stamped on it "please mishandle" or "please
handle carelessly".
</pre>
Nassim N. Taleb

    notes
    multitenant, check responsiveness, react to region failings

<h3 class="principle">4) Antifragility</h3>

What happens if an instance becomes sluggish?<br>

<table class="workloads">
<thead>
<tr><td>Type</td><td>Fix</td><td>Latency</td></tr>
</thead>
<tbody>
<tr><td>Dedicated</td><td>manual</td><td>days</td></tr>
<tr><td>VPS</td><td>manual</td><td>hours</td></tr>
<tr><td>Cloud</td><td>automatic (<code>shutdown -h now</code>)</td><td>minutes</td></tr>
</tbody>
</table>

    notes

<h3 class="principle">4) Antifragility</h3>

Crash-Oriented Programming

    notes

<h3 class="principle">
Cloud<br>
<strong>Bitdeli</strong><br>
Erlang<br>
</h3>

    notes

![image](images/bitdeli-plain.svg)<br>

    notes

<div class="archbox">
<div class="arch-title">Bitdeli backend</div>
<img class="arch" src="images/bitdeli-arch-plain.svg">
</div>

    notes

<div class="archbox">
<div class="arch-title">1) Many small instances</div>
<img class="arch" src="images/bitdeli-arch-plain-1.svg">
</div>

    notes

<div class="archbox">
<div class="arch-title">2) Avoid Disk IO</div>
<img class="arch" src="images/bitdeli-arch-plain-2.svg">
</div>

    notes

<div class="archbox">
<div class="arch-title">3) Separate Workloads</div>
<img class="arch" src="images/bitdeli-arch-plain-3.svg">
</div>

    notes

<div class="archbox">
<div class="arch-title">4) Antifragility</div>
<img class="arch" src="images/bitdeli-arch-plain-4.svg">
<div>

    notes

<h3 class="principle">
Cloud<br>
Bitdeli<br>
<strong>Erlang</strong><br>
</h3>

    notes

Why Erlang?

    notes

Fault Model

    notes

Simplicity

    notes

<h3 class="principle">Lessons learned</h3>

    notes

<h3 class="principle">Let the Erlang VM crash</h3>
Hard memory limits<br>
Out of file descriptors<br>
Disk hangs<br>
Competing processes

    notes

<h3 class="principle">Memory Efficiency</h3>
Binaries<br>
A few tactical NIFs<br>

    notes

<h3 class="principle">Weak State</h3>

Independent gen\_servers<br>
gen_servers that reconstruct their state<br>

    notes

Erlang<br>
Antifragility<br>
Challenge

    notes

Can your system survive<br>
<span style="color: white; font-size: 130%">a randomly corrupted state</span><br>
in a gen_server?<br>
<br>
<span style="font-size: 60%">(aka Chaos Monkey on LSD)</span>

    notes

Thank You<br>
![image](images/big_logo.png)

    notes
