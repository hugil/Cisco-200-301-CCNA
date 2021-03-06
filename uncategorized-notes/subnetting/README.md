# Subnetting

## The three-step subnetting process

_This process is outlined in detail in the excellent video course over at CBTNuggets by Jeremy Cioara.  
I strongly recommend you to watch it and create your own notes or use these notes supporting your learning journey._

### Step 1. Convert the number of networks to binary

Remember, subnetting is like slicing a pizza. We got to know how many slices we want to end up with.  
So the number of slices -&gt; number of networks should be converted to binary.  
  
Use this table

| Binary bits | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Decimal value by position | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

{% hint style="info" %}
**Thought process**  
You need 50 networks. 50 fall in-between 64 and 32 in the table.  
Count the bits from the highest number below 50 in the table \(32\).  
32.. 16.. 8... 4.. 2.. 1.. gives 6 bits!
{% endhint %}

###  Step 2. Reserve bits in the mask and find your increment

The CIDR notation /XX indicates the count of bits in the subnet mask, where XX is the amount.  
This is how a /24 looks like:

| Binary bits | 1 1 1 1 1 1 1 1 | 1 1 1 1 1 1 1 1  | 1 1 1 1 1 1 1 1 | 0 0 0 0 0 0 0 0 |
| :--- | :--- | :--- | :--- | :--- |
| Decimal value | 255 | 255 | 255 | 0 |

If you count the ones you will see there are 24 ones.

{% hint style="info" %}
**Thought process**  
Write out the bits just like the table above and convert them to decimal.  
If you are subnetting from a particular mask, add as many 'ones' as bits you got in Step 1.
{% endhint %}

  
Example,  
If you want to turn a /24 network into 50 networks and you followed Step 1, you have now got 6 bits.  
That should give you a /30 mask. 

Notice in the table below with 6 additional bits, the decimal value now becomes 252 after being converted from bits to binary.

| Binary bits | 1 1 1 1 1 1 1 1 | 1 1 1 1 1 1 1 1  | 1 1 1 1 1 1 1 1 | 1 1 1 1 1 1 0 0 |
| :--- | :--- | :--- | :--- | :--- |
| Decimal value | 255 | 255 | 255 | 252 |

That means a /30 mask is 255.255.255.252, check out the cheat sheet below if you don't believe me!

### Step 3. Use increment to generate network ranges

Step 3 builds on what you did in step 2, reuse the binary bits. Let's assume we're working with the same /30 mask.  
  
11111111   11111111   11111111  11111**1**00  
  
Pay attention to the last 1 in the series of bits, this is your increment value.  
**Converting it to binary gives us the value: 4**. 

Check the table in Step 1 if you are unsure.  
  
For a /30 network the size of every network will therefore be 4 - 2 = 2 hosts.  
Why -2? Because, remember.. we have 1 broadcast address and 1 network address.

When you need to spell out the ranges you increase the last octet in your network address by the increment. If you network address starts on 10.0.0.0, you would have these ranges:

| Network Range \(Start\) | Network Range \(End\) | Hosts |
| :--- | :--- | :--- |
| 10.0.0.0 | 10.0.0.3 | 2 |
| 10.0.0.4 | 10.0.0.7 | 2 |
| 10.0.0.8 | 10.0.0.11 | 2 |
| 10.0.0.12 | 10.0.0.15 | 2 |
| ...and it goes on |  |  |

Did you notice the increment defines only, and only, the start of the network ranges. This means your ending address is always -1 from the next starting address.

{% hint style="info" %}
**Wanna go crazy?**  
[Try out some subnets in the visual subnet calculator to get your thoughts spinning in the right direction!](http://www.davidc.net/sites/default/subnets/subnets.html)
{% endhint %}

## Cheat Sheet

![](../../.gitbook/assets/image%20%2818%29.png)

## Subnet characteristics

**Classful addressing**

When IP-addressing was developed there were 3 original classes

| Class | First octet range | Octets representing network port | Binary |
| :--- | :--- | :--- | :--- |
| Class C | 192 - 223 | first three octets | The value of first two binary places in the first octet must be 11. |
| Class B | 128 - 191 | first two octets | The value of first two binary places in the first octet must be 10. |
| Class A | 1 - 126 | first octet | The value of first binary places in the first octet must be 0. |

