# What is DNS?
- Is the phonebook of the Internet. Humans access information online through domain names, like nytimes.com or espn.com
- Web browsers interact through Internet Protocol (IP) addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.
- Each device connected to the Internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses such as 192.168.1.1 (in IPv4), or more complex newer alphanumeric IP addresses such as 2400:cb00:2048:1::c629:d7a2 (in IPv6).
- The Domain Name System (DNS) maps human-readable domain names (in URLs or in email address) to IP addresses.
- For example, DNS translates and maps the domain `freecodecamp.org` to the `IP` address `104.26.2.33`.
# How does DNS work?

- The process of DNS resolution involves converting a hostname (such as www.example.com) into a computer-friendly IP address (such as 192.168.1.1). An IP address is given to each device on the Internet, and that address is necessary to find the appropriate Internet device - like a street address is used to find a particular home. When a user wants to load a webpage, a translation must occur between what a user types into their web browser (example.com) and the machine-friendly address necessary to locate the example.com webpage.

- In order to understand the process behind the DNS resolution, it’s important to learn about the different hardware components a DNS query must pass between. For the web browser, the DNS lookup occurs “ behind the scenes” and requires no interaction from the user’s computer apart from the initial request.
- There are 4 DNS servers involved in loading a webpage:
  - DNS recursor - The recursor can be thought of as a librarian who is asked to go find a particular book somewhere in a library. The DNS recursor is a server designed to receive queries from client machines through applications such as web browsers. Typically the recursor is then responsible for making additional requests in order to satisfy the client’s DNS query.
  - Root nameserver - The root server is the first step in translating (resolving) human readable host names into IP addresses. It can be thought of like an index in a library that points to different racks of books - typically it serves as a reference to other more specific locations.
  - TLD nameserver - The top level domain server (TLD) can be thought of as a specific rack of books in a library. This nameserver is the next step in the search for a specific IP address, and it hosts the last portion of a hostname (In example.com, the TLD server is “com”).
  - `Authoritative nameserver`(eg. cloudfare, godaddy) - This final nameserver can be thought of as a dictionary on a rack of books, in which a specific name can be translated into its definition. The authoritative nameserver is the last stop in the nameserver query. If the authoritative name server has access to the requested record, it will return the IP address for the requested hostname back to the DNS Recursor (the librarian) that made the initial request.
# What's the difference between an authoritative DNS server and a recursive DNS resolver?
## Recursive DNS resolver
- The recursive resolver is the computer that responds to a recursive request from a client and takes the time to track down the DNS record. It does this by making a series of requests until it reaches the authoritative DNS nameserver for the requested record (or times out or returns an error if no record is found).
- Luckily, recursive DNS resolvers do not always need to make multiple requests in order to track down the records needed to respond to a client; caching is a data persistence process that helps short-circuit the necessary requests by serving the requested resource record earlier in the DNS lookup.

```
from CND Client -> DNS Recursive Resolver (Active) -> DNS Root Nameserver -> DNS TLD Nameserver -> CLoudfare.com auth nameserver
```
## Authoritative DNS server
- Put simply, an authoritative DNS server is a server that actually holds, and is responsible for, DNS resource records.
- This is the server at the bottom of the DNS lookup chain that will respond with the queried resource record, ultimately allowing the web browser making the request to reach the IP address needed to access a website or other web resources. 
-An authoritative nameserver can satisfy queries from its own data without needing to query another source, as it is the final source of truth for certain DNS records.
```
from CND Client -> DNS Recursive Resolver -> DNS Root Nameserver -> DNS TLD Nameserver -> CLoudfare.com auth nameserver -> blog.cloudfare.com auth nameserver(active)
```
# What are the steps in a DNS lookup?
- For most situations, DNS is concerned with a domain name being translated into the appropriate IP address. To learn how this process works, it helps to follow the path of a DNS lookup as it travels from a web browser, through the DNS lookup process, and back again. Let's take a look at the steps.

- Note: Often DNS lookup information will be cached either locally inside the querying computer or remotely in the DNS infrastructure. There are typically 8 steps in a DNS lookup. When DNS information is cached, steps are skipped from the DNS lookup process which makes it quicker. The example below outlines all 8 steps when `nothing is cached`.

- The `8 steps` in a DNS lookup:
  - A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a DNS recursive resolver.
  - The resolver then queries a DNS root nameserver (.).
  - The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .net), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD.
  - The resolver then makes a request to the .com TLD.
  - The TLD server then responds with the IP address of the domain’s nameserver, example.com.
  - Lastly, the recursive resolver sends a query to the domain’s nameserver.
  - The IP address for example.com is then returned to the resolver from the nameserver.
  - The DNS resolver then responds to the web browser with the IP address of the domain requested initially.
  - Once the 8 steps of the DNS lookup have returned the IP address for example.com, the browser is able to make the request for the web page:

- The browser makes a HTTP request to the IP address.
- The server at that IP returns the webpage to be rendered in the browser (step 10).
# What are the types of DNS Queries?
- In a typical DNS lookup three types of queries occur. By using a combination of these queries, an optimized process for DNS resolution can result in a reduction of distance traveled. In an ideal situation cached record data will be available, allowing a DNS name server to return a non-recursive query.

- 3 types of DNS queries:
  - Recursive query - In a recursive query, a DNS client requires that a DNS server (typically a DNS recursive resolver) will respond to the client with either the requested resource record or an error message if the resolver can't find the record.
  - Iterative query - in this situation the DNS client will allow a DNS server to return the best answer it can. If the queried DNS server does not have a match for the query name, it will return a referral to a DNS server authoritative for a lower level of the domain namespace. The DNS client will then make a query to the referral address. This process continues with additional DNS servers down the query chain until either an error or timeout occurs.
  - Non-recursive query - typically this will occur when a DNS resolver client queries a DNS server for a record that it has access to either because it's authoritative for the record or the record exists inside of its cache. Typically, a DNS server will cache DNS records to prevent additional bandwidth consumption and load on upstream servers.
# What is DNS caching? Where does DNS caching occur?
- The purpose of caching is to temporarily stored data in a location that results in improvements in performance and reliability for data requests.
- DNS caching involves storing data closer to the requesting client so that the DNS query can be resolved earlier and additional queries further down the DNS lookup chain can be avoided, thereby improving load times and reducing bandwidth/CPU consumption. DNS data can be cached in a variety of locations, each of which will store DNS records for a set amount of time determined by a `time-to-live (TTL)`.

## Browser DNS caching
- Modern web browsers are designed by default to cache DNS records for a set amount of time. the purpose here is obvious; the closer the DNS caching occurs to the web browser, the fewer processing steps must be taken in order to check the cache and make the correct requests to an IP address.
- When a request is made for a DNS record, the browser cache is the first location checked for the requested record.

- In chrome, you can see the status of your DNS cache by going to `chrome://net-internals/#dns`.

## Client Operating system (OS) level DNS caching
- The operating system level DNS resolver is the second and last local stop before a DNS query leaves your machine. The process inside your operating system that is designed to handle this query is commonly called a “stub resolver” or DNS client.
- When a stub resolver gets a request from an application, it first checks its own cache to see if it has the record. If it does not, it then sends a DNS query (with a recursive flag set), outside the local network to a DNS recursive resolver inside the Internet service provider (ISP).

- When the recursive resolver inside the ISP receives a DNS query, like all previous steps, it will also check to see if the requested host-to-IP-address translation is already stored inside its local persistence layer.

- The recursive resolver also has additional functionality depending on the types of records it has in its cache:

  - If the resolver does not have the A records, but does have the NS records for the authoritative nameservers, it will query those name servers directly, bypassing several steps in the DNS query. This shortcut prevents lookups from the root and .com nameservers (in our search for example.com) and helps the resolution of the DNS query occur more quickly.
  - If the resolver does not have the NS records, it will send a query to the TLD servers (.com in our case), skipping the root server.
  - In the unlikely event that the resolver does not have records pointing to the TLD servers, it will then query the root servers. This event typically occurs after a DNS cache has been purged.
# History

- Host-to-host communication within the same network wasn’t reliable enough. TCP/IP helped solve this issue:
  - Transmission Control Protocol (TCP) provides quality assurance measures for the process of turning messages (between hosts) into packets.
  - The TCP protocol is connection-oriented, which means a connection between source host and destination host must be established.
  - Internet Protocol (IP) defines how messages (packets) are carried between source host and destination host. An IP address is a unique identifier for a specific path that leads to a host on a network.
  - TCP and IP work closely together, which is why they’re usually referenced like “TCP/IP.”

# Domain Names

- In the context of DNS, a domain name provides a user-friendly way to point to non-local resources. This could be a website, a mail system, print server, or any other server that is available on the Internet. A domain name can be more than just a website!
- A domain name is much easier to remember and enter into a terminal or Internet browser, than an IP address.

- A domain name is part of a Uniform Resource Locator (URL), but the terms are not synonymous. A URL is the complete web address of a resource, while the domain name is the name of a website and is a sub-component of every URL.

- While there are technical distinctions between URLs and domain names, web browsers usually treat them the same way, so you’ll get to the website if you type in the complete web address, or just the domain name.

# Top Level Domains and Second Level Domains

- There are two parts to any given domain: top-level domain (TLD) and second-level domain (SLD). The parts of a domain name become more specific when moving from the right (end) to the left (beginning).

- This can be confusing at first. For example, let’s look at “freecodecamp.org”
  - URL: https://www.freecodecamp.org
  - Domain name: freecodecamp.com
  - TLD: org
  - SLD: freecodecamp
- In the early days of ARPAnet, there were a limited number of TLDs available, including com, edu, gov, org, arpa, mil, and 2-letter country code domains. These TLDs were initially reserved for institutions participating in the ARPAnet, but some later became available on commercial markets.

- Today, there is a comparative wealth of available TLDs, including net, aero, biz, coop, info, museum, name, and others.

- Second-level domains are the domains that are available for individual purchase through domain registrars (for example, Namecheap).

# IP Addresses (IPv4)
- The IPv4 address is a 32-bit number that uniquely identifies a network interface on a machine. An IPv4 address is typically written in decimal digits, formatted as four 8-bit fields that are separated by periods. Each 8-bit field represents a byte of the IPv4 address. This form of representing the bytes of an IPv4 address is often referred to as the dotted-decimal format.
- While IP addresses are related to DNS in their function, the Internet Protocol itself is technically separate from DNS. I’ve already provided historical context for this distinction, so now I’ll explain how IP addresses function.

- An `IP address`, as previously mentioned, is a `unique identifier` for a specific path that leads to a `host` on a `network`. I’d like to reference the analogy of a phone number and a phone: a phone number doesn’t represent the phone itself, it’s just a way to reach the person with the phone.

- This analogy is reasonably appropriate (at least, on a surface level), with IP addresses. An IP address represents an endpoint, but it isn’t the endpoint itself. IP assignments can be `fixed` (permanent) or `dynamic` (flexible and may be reassigned).

- Like a domain name, the organization of IP addresses follows a `hierarchical structure`. Unlike domain names, IP addresses get more specific going left-to-right. This is an IPv4 example below:
```
129.144.       50.56
  networkpart    host part
```
  - Network: The network part specifies the unique number that is assigned to your network. The network part also identifies the class of network that is assigned. In Figure 5–3, the network part occupies two bytes of the IPv4 address.
  - Host: This is the part of the IPv4 address that you assign to each host. The host part uniquely identifies this machine on your network. Note that for each host on your network, the network part of the address is the same, but the host part must be different.

# How many IP addresses are there?
- IPv4 was the very first iteration of IP that ARPAnet used in production. Deployed in the early 80s, it’s still the most prevalent IP version. It’s a `32-bit` scheme, and can therefore support slightly over `4 billion addresses`.

- `IPv6` has a `128-bit` scheme, which allows it to support 340 undecillion addresses. It also offers performance improvements on IPv4.

- Example IPv4 address:
  ```
  104.26.2.33 (freeCodeCamp)
  ```
- Example IPv6 address:
  ```
  2001:db8:a0b:12f0::1 (the compressed format and not pointing to freeCodeCamp)
  ```
# How does the Domain Name System work?
## The Domain Namespace
- This tree graph, with the root at the top, best illustrates the structure:
```
                  root
        com               org           gov
    freecodecamp        xx  xx   xx    xx  xx
subdomain1 subdomain2
```
- The top of this graph, noted with a “.” is called the `root.`
- The root domain has a zero-length label.
- The first level down from the root are the TLDs: `the com, org, edu, and gov`. Please note that this graph does not contain a full list of TLDs.
- Below TLDs are the SLDs, the second-level domains. The children of each node are called “subdomains,” which are still considered part of the parent domain. For example, in `freecodecamp.org`, `freecodecamp (the SLD)` is a `subdomain of org (the TLD)`.
## Domain Name Servers
- At this point is where thinking about a client-server relationship, at least initially, is useful. Domain nameservers are the `server` side of the client-server relationship. 
- Nameservers may load one, hundreds, or even thousands of zones, but they never load the entire namespace. Once a nameserver has loaded the totality of a zone, it is said to be authoritative for that zone.
- To understand why nameservers function the way they do, it’s useful to understand the “client” part of the relationship.
### Resolvers
- In DNS, the client (the requester of information) is called the `resolver` which may seem backward at first. Wouldn’t the server that is resolving the request be called the “resolver?” I thought so, too, but it’s not. Best to just memorize that and move on.

- Resolvers are typically included, de facto, in most operating systems, so the applications installed on the OS don’t have to figure out how to make low-level DNS queries.

- DNS queries and their responses are types of DNS messages, and have their own data transport protocol (usually UDP). Resolvers are responsible for helping applications installed on the OS `translate requests for DNS-related data into DNS queries`.

- In sum, `resolvers` are responsible for `packaging and sending off requests for data`. Once the resolver receives the response (if at all), it passes that back to the original requesting application in a format consumable to the requesting application.
### Back to Nameservers
- Now that we are a bit more familiar with the client-side of the relationship, we need to understand how domain nameservers respond to resolver queries.

- Nameservers respond to DNS queries through `resolution`. Resolution is the process by which nameservers find datafiles in the namespace. Depending on the type of query, nameservers respond differently to different queries, but the end goal is resolution.
### Query Types
- Type of query? Yes, there are multiple types of DNS queries. But first, what’s usually in a DNS query? It’s a request for information, specifically for the `IP address associated with a domain name`.

  - `Recursive`: recursive queries allow the query to be referred on to multiple nameservers to be resolved. If the first queried nameserver doesn’t have the desired data, then that nameserver sends the query along to the most appropriate next nameserver, until the nameserver with the desired datafiles is found and sends a response to the resolver.

  - `Iterative`: iterative queries require the queried nameserver to respond either with the desired data or with an error. The response may contain the IP address of the most appropriate nameserver to send the request to next; the resolver may then send another request to that, more appropriate, nameserver.
- In case you need it, you can also query for the domain name, if all you have is the IP address. This is called a reverse DNS lookup.

- Once the query reaches a nameserver that contains the desired datafiles, then the query can be resolved. Nameservers have a number of datafiles associated with them, all or some of which may be used to resolve the query.

### Resource Records (RRs)
- These are the datafiles in the domain namespace. These datafiles have specific formats and contents.

- The most common RRs:

  - A Record: if you haven’t heard of any other RRs except for this one, that would make sense. It’s likely the best-known RR and contains the IP address of the given domain.
  - CNAME Record: if you haven’t heard of any other RRs except for this one and the A record, that would also make sense. The “C” stands for “canonical”, and is used instead of an A record, to assign an alias to a domain.
SOA Record: this record contains administrative information about the one, including the email address of the administrator. Hint: if you administer a zone, make sure there’s a valid email address here, so folks can get in touch with you if needed.

### Caching and Time to Live (TTL)
- When the local nameserver receives a response from a query, it caches that data (stores it in memory), so next time it receives the same query, it can just answer the query directly rather than go through the original, longer resolution process.

- But once this information is cached, it is both static and isolated, and is therefore at risk of becoming out of date. Therefore, resource records all have what is called a time to live (TTL) value, which dictates how long that data can be cached. When that time runs out (reaches zero), the nameserver deletes the record.

- Important note: TTL doesn’t apply to the name servers that are authoritative for the zone that contains the resource record. It just applies to the nameserver that cached that resource record.
# A Day in the Life of a Query
- Nameserver A receives a recursive query form the resolver (client side)
- A sends an iterative query to B
- B Refers A to other nameservers, including C
- A sends an iterative query to C
- C refers A to other nameservicers, including D
- D anwsers
- A return anwser to resolver
# What is an A record?

- An A record (or ‘address record’) specifies which IP is assigned to a particular domain. This entry doesn’t necessarily have to be made – a domain can for example be used only for mail services – so an A record for this domain is not necessary.

- Alternatively, more than one record can be entered for each domain. In this case, a new record is returned for each query. This is particularly important for large scalable systems.
- Depending on the hierarchy of the website, there may be `third-, fourth, fifth- level` domains.
- For example, in hypothetical-subdomain .freecodecamp.org, hypothetical-subdomain is the third-level domain, and the subdomain of freecodecamp. So on and so forth, at least up to `127` levels, which is the maximum allowed by DNS.

# How do I point my domain name to an IP address?

- Login to your domain management
- Scroll down to the Advanced Domain Settings section and click on the `Manage DNS (A, MX, CNAME, TXT)` link.
- From the Advanced DNS tab -> Select `A` from the `Type` drop down list in the `Add` new entry section.
- In the Hostname field enter `www` -> In the Destination IPv4 address field enter the IP address the domain will point to.
- Please note: You can also create a `Blank` Record alongside your original A Record by entering an `@` symbol instead of www. This will mean that people can enter example.com into their browser and be directed to your IP address, whereas entering `www` will mean that the user will have to enter `www.example.com`.

# How can I point a subdomain to an IP address?

- Firstly, you need to ensure your domain is pointed to the 123 Reg nameservers.

- If the domain is not pointed to the 123 Reg nameservers, you will be unable to manage them from the 123 Reg control panel.
- Steps:
  - Login to your domain management. In the Domain names section, select the `relevant domain name` in the drop-down list and click on the Managebutton.
  - Scroll down to the Advanced Domain Settings section and click on the `Manage DNS (A, MX, CNAME, TXT)` link.
  - Select `A` from the Type drop down list in the `Add` new entry section.
  - In the Hostname field enter your chosen subdomain i.e `mail.***.com`
  - In the Destination IPv4 address field enter the `IP address` the `subdomain` will point to.
  - Click on the Add new entry button to save the new record.


# What is a DHCP Server?
- A DHCP server (Dynamic Host Configuration Protocol)  is a server that automatically assigns IP addresses to computers and other devices on the network. Without a DHCP server, each device on the network would need to be manually configured with an IP address.
- Every routers have a  built-in DHCP service
- Why is a DHCP server needed?
  - Every device on the network needs an IP address to access network resources such as the internet, applications and even making phone calls. With a DHCP server this entire process is automated and can be managed from a centralized server.
  - When mobile devices move from one office to another it may require a new IP address. DHCP handles this automatically providing a new IP addresses when the device moves to another location. Without a DHCP server there would be an overwhelming amount of manual configuration assigning IP addresses to devices on the network. A DHCP server is a huge time saver.
- Steps of create the settings:
  - Step 1: Open Server Manager
  - Step 2: Add roles and features
  - Step 3: Select Role-based or feature-based installation
  - Step4: Select destination server
  - Step 5: Select server roles
  - Step 6: Feature, DHCP Server
  - Step 7: Confirmation
- Steps of config DHCP server
  - IP4 -> Obtain dynamic IP Address

- DHCP server assignes the IP Address as a `lease`
- `Lease` is the amount of time an IP ADdress is assigned to a computer (can be 1 ,2.. days)
- The `lease` make sure the DHCP server does not run out of IP Addresses.

# Notes

- Please note: It will take between 24-48 hours for any new nameserver (DNS) records to become active
