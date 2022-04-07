# Natural Language Password
Passwords are an unfortunate part of our everyday lives. If you're doing things right you likely have hundreds of passwords and hopefully you have a password manager.  How many times have you been in a position where you need one of these randomly generated passwords from your password manager but there's no option to copy/paste to your destination. Now you're stuck typing this:
```
hkUn9TBgf28%S0e$Qw#3zRO^
```
Phrases are so much easier to remember and transcribe. I.e. "The Quick Brown Fox Jumps" is a lot easier to remember and transcribe, but it still might be easily guessable.  I tried a handful of techniques for coming up with good passphrases instead of passwords but then I ran across this idea of a "natural language password." It's still randomly generated using the concept of [Diceware](https://theworld.com/~reinhold/diceware.html) but it focuses on the idea of adjective/noun pairs. Ray Eads did a presentation on this concept for Linux Fest Northwest which you can watch [here](https://youtu.be/QW4tSTiDCT8) and I encourage you to do so. His database of nouns and adjectives is what powers this script which I believe he's maintaining here: <https://github.com/NaturalLanguagePasswords/system>

I got a lot of help from [Tim Evans' blog](https://www.timmevans.net/blog/generating-diceware-passphrases-with-powershell/) on generating diceware passphrases with Powershell. It was actually this article about the effectiveness of the Get-Random cmdlet that ultimately lead me to Tim's blog entry: <https://powershellmagazine.com/2014/07/28/testing-the-effectiveness-of-get-random/>

These are all worth reading.

# New-NaturalLanguagePassword
This script is intended as a standalone file. Meaning you don't need separate files containing your wordlists. Unfortunately that means the script is over 9000 lines long, but you don't really need to read it to use it. I was more interested in portability and ease of use. To get started you can simply execute the script from a Powershell prompt by itself
```Powershell
PS$> .\New-NaturalLanguagePassword
bamboo toggle lazy airline
```
You can also use Get-Help against the script to read about the parameters and how to use it.

## Parameter Pairs
It generates Adjective/Noun pairs, this defines how many pairs you want returned. The default is 2 pairs (four words)
## Parameter Complexity
Select if you would like the complexity to include upper case beginning characters for each word, or common character substitution, or both.
## Parameter Shortcut
A switch parameter to be used if calling this script from a shortcut link. The Target in the shortcut would look like this if the shortcut was in the same directory as this script:
powershell.exe -noprofile -exec b -command "& {Clear; .\Get-NaturalLanguagePassword.ps1 -pairs 3 -Shortcut}"

This will cause the script to leave the window open for the administrator to copy/paste the password. Then they can press 'Enter' and the window will close.
## Parameter Prepend
Provide a string you would like prepended to the password output
## Parameter Append
Provide a string you would like appended to the password output  
## Parameter NoSpace
This switch parameter will remove all spaces from the passphrase.  Goes nicely with "-Complexity UpperCase" for a camelcase passphrase.  
## Example  
One of the ways I use this script on the daily is to generate a couple dozen passphrases and then I'll select one that I think is more memorable.
```
PS$> 1..20 | %{.\New-NaturalLanguagePassword -Append '1$6&'}
powered importer low mammary1$6&
ashy article detached army1$6&
armored alley harmful violence1$6&
flaxen scrolls mighty flub1$6&
muggy supper festive prism1$6&
dreamy shove crispy consoles1$6&
chalky cleavers strict clavicle1$6&
faded diploma mute garnet1$6&
fatal secretary curly creel1$6&
filthy leech swampy consumer1$6&
amusing spinner chubby duckling1$6&
clear duke factual hairs1$6&
popular faxes surplus egotism1$6&
blond members swank locusts1$6&
hot ploy foreign booze1$6&
inner bellies mushy weirdo1$6&
joyous naturist undated offers1$6&
fishy heroes returned lists1$6&
brittle satchel crazed lair1$6&
dreaded collage wrinkly tampon1$6&
```
It's a bit of shorthand but in Powershell "1..20" will produce an array of 20 numbers, which I'm then piping to an alias (%) for ForEach-Object. I'm saying that for each number that comes through the pipe, execute the script. The numbers are meaningless, it's just a way to repeat the script quickly. 

If you're really big on character substitution you can add that and maybe just do one pair for something random and memorable.
```
PS$> .\New-NaturalLanguagePassword -Complexity Both -Pairs 1
N3rv0u$ $3rv1c3
```