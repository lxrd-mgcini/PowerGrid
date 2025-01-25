# Dumping-a-domains-worth-of-passwords-with-mimikatz-pt-2

A year ago, @mubix published a post on http://carnal0wnage.attackresearch.com/ about “Dumping a domain’s worth of passwords with mimikatz“. In the article, he talked about using a combination of PowerShell, file shares, .bat scripts and output files in order to run Mimikatz across a large number of machines in an enterprise using just WMI.

A few months ago, @obscuresec posted a great article on using PowerShell as a quick and dirty web server. I started thinking about how to incorporate Chris’ work with Rob’s approach to simplify the attack flow a bit.

The result is Invoke-MassMimikatz, a PowerShell script that utilizes @clymb3r’s work with reflective .dll injection/Mimikatz, along with @obscuresec’s webserver and WMI functionality to deliver Mimikatz functionality en-mass to machines on a domain. Again, this doesn’t rely on PSRemoting, and doesn’t need any external binaries, though it does need local admin. It’s just pure PowerShell, WMI, and HTTP goodness.

Here’s how Invoke-MassMimikatz works:

A jobbified web server is spun up in the background. This server will share out the Invoke-Mimikatz code for GET requests, and decodes POST responses with results from targets. It defaults to port 8080, which can be changed with the -LocalPort flag.
A PowerShell one-liner is built that uses the IEX download cradle to grab/execute code from the server, encode the results in Base64, and then post the results back to the same server.
The command is executed on all specified hosts using WMI.
As the raw results come back in clients, the raw output is saved to a specified folder, under “HOSTNAME.txt”. This folder defaults to “MimikatzOutput”, which can be changed with the -OutputFolder flag.
Some parsing code tries to aggregate the result sets and build custom psobjects of credential sets.

End result? You get some nice “server”/”credential” results pouring back in, which can be piped to CSVs or whatever you would like.

Let me know if you find this useful!
