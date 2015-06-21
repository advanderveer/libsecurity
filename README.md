# libsecurity

When we're talking about security, the internet is the true wild wild west of today and the problems doesn't seem to be disappearing anytime soon. Until we find a way to create bulletproof server software we'll need a system in place to react as quick as possible to the release of a new 0-day vulnerability. 

Traditionally it can be very difficult for a software vendor to inform their consumers. Especially for open source projects, the product is often acquired (anonymously) through a variety of channels and contacting the user can be downright impossible. Docker can provide a solution, as an universal runtime it can also act as a real time channel for receiving and acting on new vulnerabilities.

## How does it work
fundamental to the workings of libsecurity is the involvement two seperate parties: the vendor and the consumer. The vendor releases new versions of software and is responsible for fixing vulnerability issues and broadcasting the existence of such vulnerability to the consumers. 

### The Vendor

For this party, libsecurity provides a container that allows vendors to test certain images for the existence of a vulnerability on any of the images that are managed by Docker:

```
docker run -v /var/run/docker.sock:/var/run/docker jerbi/cve-check
```

The container will output an example message that the vendor can broadcast across any distributed messaging platform, in this case it tells us that Docker image "9e1ed860cc088ae4b68ce28fb8888739652729e1107054f58dff90979f7dc935" is vulnerable to "CVE-2014-6271": the imfamous Shellshock vulnerability:

```
CVE-2014-6271 in 9e1ed860cc088ae4b68ce28fb8888739652729e1107054f58dff90979f7dc935
```

The vendor is reponsible for broadcasting it across a messaging platform, this demo uses twitter but one could imagine more secure channels such as irc bots or the Docker hub.

[image of twitter posting]

### The Consumer
The consumer, on his part, requires to run a container that monitors certain twitter feeds for new vulnerabilities. The consumer can decide what Twitter user to follow. For example, inside a corporate network one might want to watch to the twitter feed of the security office (advanderveer).

```
docker run -it -v /var/run/docker.sock:/var/run/docker.sock advanderveer/docksec --twitter_user=advanderveer
```

Whenever a message such as _"CVE-2014-6271 in 9e1ed860cc088ae4b68ce28fb8888739652729e1107054f58dff90979f7dc935"_ is broadcasted across the network and picked up by the container above it will attempt two things:

1. x
2. y


