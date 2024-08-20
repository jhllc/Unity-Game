# GameHacking.gg

## Unity games
Today, we are going to look at a Unity game. We are going to use dnSpyEx for reading and editing the source code, and we are 
going to use Cheat Engine as our debugger. The game has not been release, yet, and was only available at defcon, but will 
be released, possibly with additions, eventually. You can check back here, or https://gamehacking.gg/ for updates, on that.

### [dnSpyEx](https://github.com/dnSpyEx/dnSpy/releases)
Above is a link to the version of `dnSpyEx` that I downloaded and installed. After installing it, you will need to install 
the Unity game you want to RE, and then you need to navigate into the location of the actual game code, or what is unique 
to the particular game, is located at `GAMENAME\GAMENAME_Data\Managed` where `GAMENAME` is the actual name of the game you
installed. In our case that is `GameHackingGG\GameHackingGG_Data\Managed`.  Inside this is `Assembly-CSharp.dll`. We will 
drag that file into `dnSpyEx`, and see what's in it! The first thing we see, is, an anticheat class.
<br/>
<img alt="Level 4 DNSpy" src="img/L0 dnSpy anticheat.png" title="DNSpy IL COde" />
<br/>
We can actually stub most of this, although I think, by looking at the [Unity documentation](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html)
we can see that `MonoBehaviour` classes have a `Start` and `Update` function. I assume those are really the only two functions
that need to be stubbed out, but I also replaced the `GetHashOfCode` function to return an empty string, and the `IsCheatProcessRunning`
to return true, anyways, just because it's pretty easy to do. (Right click each function and use `Replace Method Body with 
stub...` menu option. I just had to edit the `GetHashOfCode` function to return empty string, as it return `null` by default

All you have to do is right click the code you want to edit, click `Edit IL Instructions...` and change it to ldstr, and 
it automatically loads an empty string for return.
<br/>
<img alt="Level 4 DNSpy" src="img/L0 dnSpy anticheat stubbed.png" title="DNSpy IL COde" />
<br/>

You must select the module and then go to `File > Save Module` for your changes to take place.

### [Cheat Engine](https://www.cheatengine.org/)
Cheat Engine is a fantastic dynamic analysis and debugging tool that is absolutely SLEPT on outside of the modding/cheating 
community. Even though it has "Cheat" in the name, it's really just a debugger and memory viewer that has x86 assembly,
lua and C as a scripting language. It also comes with some really cool tutorials, so, you should check those out, too, if
you haven't, already! 

Make SURE you skip all of the adware when you install this tool. It is a free tool, but, only free because of the advertisements
and software "bundled" with Cheat Engine, of which you can clikc "Skip All" to skip all of them, at the start of installation.

We also will want to go into our settings, and make hotkeys for the `next scan` types. I like to bind `Decrease Value` to
F1, `Increase Value` to F2, `Changed Value` to F3 and `Unchanged Value` to F4. These will allow you to quickly scan the game
as you are in it, via hotkey.
<br/>
<img alt="CE Settings" src="img/L0 CE Settings.png" title="CE Settings" />
<br/>
More about CE will be explained as these levels progress.
