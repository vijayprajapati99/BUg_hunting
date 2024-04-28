# BUg_hunting

#!/bin/bash

# Discover subdomains
subfinder -d <target_domain> -silent | tee subdomains.txt

# Discover URLs from the web archive
cat subdomains.txt | waybackurls | tee urls.txt

# Scan for XSS vulnerabilities
cat urls.txt | dalfox pipe | tee xss_results.txt

# Test XSS filters
cat xss_results.txt | noxss | tee filtered_results.txt

# Test for reflected XSS
cat filtered_results.txt | xsstrike.py -m GET --random-agent | tee reflected_xss_results.txt

# Test for stored XSS
cat filtered_results.txt | xsstrike.py -m POST --random-agent | tee stored_xss_results.txt


ce installed, you can use the tool to find subdomains of a target domain. For example, to find subdomains of example.com, run:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com
You can also use the -o flag to save the output to a file:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -o subdomains.txt
To find subdomains of multiple domains, you can use the -dL flag and provide a list of domains:
Verify
Edit
Full Screen
Copy code
subfinder -dL domains.txt
You can also use the -silent flag to hide unnecessary output:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -silent
To find subdomains of a target domain using a specific template, you can use the -t flag:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -t technologies
To find subdomains of a target domain using a specific source, you can use the -s flag:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -s censys
To find subdomains of a target domain using a specific resolver, you can use the -r flag:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -r 8.8.8.8
To find subdomains of a target domain using a list of resolvers, you can use the -rL flag:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -rL resolvers.txt
To find subdomains of a target domain using a specific output format, you can use the -oF flag:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -oF json
To find subdomains of a target domain using a specific output file, you can use the -o flag:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -o subdomains.json
To find subdomains of a target domain using a specific output directory, you can use the -oD flag:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -oD output
To find subdomains of a target domain using a specific output file and format, you can use the -o and -oF flags:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -o subdomains.json -oF json
To find subdomains of a target domain using a specific output file, format, and directory, you can use the -o, -oF, and -oD flags:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -o subdomains.json -oF json -oD output
To find subdomains of a target domain using a specific output file, format, directory, and resolver, you can use the -o, -oF, -oD, and -r flags:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -o subdomains.json -oF json -oD output -r 8.8.8.8
To find subdomains of a target domain using a specific output file, format, directory, resolver, and source, you can use the -o, -oF, -oD, -r, and -s flags:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -o subdomains.json -oF json -oD output -r 8.8.8.8 -s censys
To find subdomains of a target domain using a specific output file, format, directory, resolver, source, and template, you can use the -o, -oF, -oD, -r, -s, and -t flags:
Verify
Edit
Full Screen
Copy code
subfinder -d example.com -o subdomains.json -oF json -



Answer
2
3

Bug_hunt/subfinder-dev/ $ ls DISCLAIMER.md Dockerfile LICENSE.md README.md static/ THANKS.md v2/ Bug_hunt/subfinder-dev/ $ how to setup this sub finder

Edit

To set up subfinder in your local environment, follow these steps:

Clone the subfinder repository from GitHub:
Verify
Edit
Full Screen
Copy code
git clone https://github.com/projectdiscovery/subfinder.git
Move into the subfinder directory:
Verify
Edit
Full Screen
Copy code
cd subfinder
Check the version of Go installed on your system:
Verify
Edit
Full Screen
Copy code
go version
If you don't have Go installed, install it from the official website: https://golang.org/dl/

Set up the Go workspace:

Verify
Edit
Full Screen
Copy code
mkdir -p $HOME/go/src $HOME/go/bin
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$PATH
Install the required dependencies:
Verify
Edit
Full Screen
Copy code
go get -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder
Build the subfinder binary:
Verify
Edit
Full Screen
Copy code
go build -v -o subfinder v2/main.go
Verify the installation by checking the version of subfinder:
Verify
Edit
Full Screen
Copy code
./subfinder version
You can now use subfinder to find subdomains of a target domain:
Verify
Edit
Full Screen
Copy code
./subfinder -d example.com
To make subfinder available system-wide, move the binary to a directory in your PATH:
Verify
Edit
Full Screen
Copy code
sudo mv subfinder /usr/local/bin/
Now, you can use subfinder from any directory in your terminal.

Note: If you are using GitHub CS50 managed repository, you may need to follow the instructions in the README to enable Git and use the tool.




Answer
2
3

SCLAIMER.md Dockerfile LICENSE.md README.md static/ THANKS.md v2/ Bug_hunt/subfinder-dev/ $ go version bash: go: command not found Bug_hunt/subfinder-dev/ $ go version bash: go: command not found

Edit

It seems like Go is not installed on your system. To install Go, follow these steps:

Download the latest version of Go from the official website: https://golang.org/dl/

Extract the downloaded archive:

Verify
Edit
Full Screen
Copy code
tar -xvf go<version>.linux-amd64.tar.gz
Replace <version> with the actual version number you downloaded.

Move the extracted directory to a suitable location:
Verify
Edit
Full Screen
Copy code
sudo mv go /usr/local
Set up the Go workspace:
Verify
Edit
Full Screen
Copy code
mkdir -p $HOME/go/src $HOME/go/bin
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$PATH
Add the Go binary directory to your PATH:
Verify
Edit
Full Screen
Copy code
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
Reload your terminal:
Verify
Edit
Full Screen
Copy code
source ~/.bashrc
Verify the installation by checking the version of Go:
Verify
Edit
Full Screen
Copy code
go version
Now that Go is installed, you can follow the previous instructions to set up subfinder.




Answer
2
3

_hunt/ $ ls dev.zip gigachat.xml subfinder-dev/ Bug_hunt/ $ cd subfinder-dev Bug_hunt/subfinder-dev/ $ ls DISCLAIMER.md Dockerfile go1.22.2.linux-amd64.tar.gz LICENSE.md README.md static/ THANKS.md v2/ Bug_hunt/subfinder-dev/ $ go build -v -o subfinder v2/main.go package v2/main.go is not in std (/usr/local/go/src/v2/main.go) Bug_hunt/subfinder-dev/ $ cd .. Bug_hunt/ $ go get -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder go: go.mod file not found in current directory or any parent directory. 'go get' is no longer supported outside a module. To build and install a command, use 'go install' with a version, like 'go install example.com/cmd@latest' For more information, see https://golang.org/doc/go-get-install-deprecation or run 'go help get' or 'go help install'. Bug_hunt/ $

Edit

It seems like you are trying to build subfinder from the source code, but you are encountering some errors. To resolve these issues, follow these steps:

Extract the go1.22.2.linux-amd64.tar.gz archive:
Verify
Edit
Full Screen
Copy code
tar -xvf go1.22.2.linux-amd64.tar.gz
Move the extracted directory to a suitable location:
Verify
Edit
Full Screen
Copy code
sudo mv go /usr/local
Set up the Go workspace:
Verify
Edit
Full Screen
Copy code
mkdir -p $HOME/go/src $HOME/go/bin
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$PATH
Add the Go binary directory to your PATH:
Verify
Edit
Full Screen
Copy code
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
Reload your terminal:
Verify
Edit
Full Screen
Copy code
source ~/.bashrc
Verify the installation by checking the version of Go:
Verify
Edit
Full Screen
Copy code
go version
Move into the subfinder-dev directory:
Verify
Edit
Full Screen
Copy code
cd subfinder-dev
Build the subfinder binary:
Verify
Edit
Full Screen
Copy code
go build -v -o subfinder v2/main.go
Verify the installation by checking the version of subfinder:
Verify
Edit
Full Screen
Copy code
./subfinder version
You can now use subfinder to find subdomains of a target domain:
Verify
Edit
Full Screen
Copy code
./subfinder -d example.com
To make subfinder available system-wide, move the binary to a directory in your PATH:
Verify

Edit
Full Screen
Copy code
sudo mv subfinder /usr/local/bin/
Now, you can use subfinder from any directory in your terminal.

Note: If you are using GitHub CS50 managed repository, you may need to follow the instructions in the README to enable Git and use the tool.




Answer
2
3

Bug_hunt/ $ cd subfinder-dev Bug_hunt/subfinder-dev/ $ go build -v -o subfinder v2/main.go package v2/main.go is not in std (/usr/local/go/src/v2/main.go) Bug_hunt/subfinder-dev/ $

Edit

Sources: geeksforgeeks.org (1) blog.projectdiscovery.io (2) securitytrails.com (3) github.com (4)

To set up the subfinder tool in the Bug_hunt/subfinder-dev/ directory, you can follow these steps:

Make sure you have Go installed on your system. If not, you can download and install it from the official website: https://golang.org/dl/
Extract the go1.22.2.linux-amd64.tar.gz file in the Bug_hunt/subfinder-dev/ directory using the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
tar -xzvf go1.22.2.linux-amd64.tar.gz
Move the extracted go directory to /usr/local/ using the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
sudo mv go /usr/local/
Set the GOROOT and GOPATH environment variables using the following commands:
bash
Verify
Edit
Run
Full Screen
Copy code
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
Add the Go bin directory to your PATH environment variable using the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
Change to the subfinder-dev/v2/cmd/subfinder directory using the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
cd v2/cmd/subfinder
Build the subfinder binary using the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
go build -v -o subfinder .
Move the built binary to /usr/local/bin/ using the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
sudo mv subfinder /usr/local/bin/
Verify that the installation was successful by running the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
subfinder -h
This should display the help message for the subfinder tool.

Note: The above steps assume that you are using a Linux-based system. If you are using a different operating system, the installation process may vary.




Answer
2
3

python tool which collect websites usings dorks

Edit

To collect websites using dorks, you can use a Python tool called Google-Dorks-Automater. This tool automates the process of searching for websites using Google dorks and saves the results to a file.

Here are the steps to use Google-Dorks-Automater:

Install the required packages:
bash
Verify
Edit
Run
Full Screen
Copy code
pip install requests beautifulsoup4
Download the Google-Dorks-Automater script from the following GitHub repository: https://github.com/maurosoria/dirsearch/blob/master/tools/Google-Dorks-Automater.py
Save the script to a file named Google-Dorks-Automater.py.
Open the script in a text editor and modify the following variables:
dorks_file: The path to a file containing the Google dorks to search for.
output_file: The path to a file where the results will be saved.
num_results: The number of results to retrieve for each dork.
user_agent: The user agent string to use when making requests to Google.
Save the changes and close the text editor.
Run the script using the following command:
bash
Verify
Edit
Run
Full Screen
Copy code
python Google-Dorks-Automater.py
The script will search for websites using the Google dorks specified in the dorks_file and save the results to the output_file.

Note: The Google-Dorks-Automater script uses the Google search API, which has a limit on the number of requests that can be made per day. If you exceed this limit, you may receive an error message.

Also, keep in mind that using Google dorks to search for websites can be considered a form of hacking, and it is important to use this tool responsibly and only for legal purposes.




Answer
2
3
Scroll to bottom

Continue

Copy Link to Share Chat

New Chat

Code
