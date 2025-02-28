# Natural Language Password
Passwords are an unfortunate part of our everyday lives. If you're doing things right you likely have hundreds of passwords and hopefully you have a password manager.  How many times have you been in a position where you need one of these randomly generated passwords from your password manager but there's no option to copy/paste to your destination. Now you're stuck typing this:
```
hkUn9TBgf28%S0e$Qw#3zRO^
```
Phrases are so much easier to remember and transcribe. I.e. "The Quick Brown Fox Jumps" is a lot easier to remember and transcribe, but it still might be easily guessable.  I tried a handful of techniques for coming up with good passphrases instead of passwords but then I ran across this idea of a "natural language password." I started with the idea of generating them as closely in methodology to [Diceware](https://theworld.com/~reinhold/diceware.html) as I could but ended up changing it to a just a RNG. Ray Eads did a presentation on the concept of Natural Language Passwords for Linux Fest Northwest which you can watch [here](https://youtu.be/QW4tSTiDCT8) and I encourage you to do so. His database of nouns and adjectives is what powers this script which I believe he's maintaining here: <https://github.com/NaturalLanguagePasswords/system>

Originally I got a lot of help from [Tim Evans' blog](https://www.timmevans.net/blog/generating-diceware-passphrases-with-powershell/) on generating diceware passphrases with Powershell. Matt Graeber's blog post was a big influence on the random number generation: <https://powershellmagazine.com/2014/07/28/testing-the-effectiveness-of-get-random/>

These are all worth reading.

# New-NaturalLanguagePassword
This script is intended as a standalone file. Meaning you don't need separate files containing your wordlists. Unfortunately that means the script is over 9000 lines long, but you don't really need to read it to use it. I was more interested in portability and ease of use. To get started you can simply execute the script from a Powershell prompt by itself
```Powershell
PS$> .\New-NaturalLanguagePassword.ps1
bamboo toggle lazy airline
```
You can also use Get-Help against the script to read about the parameters and how to use it.

## Parameter Pairs
It generates Adjective/Noun pairs, this defines how many pairs you want returned. The default is 2 pair (two words)
## Parameter TitleCase
Switch parameter to toggle the use of title case. E.g. The First Letter Of Every Word Is Uppercase. 
## Parameter Substitution
Switch parameter to toggle common character substitution.  E.g. '3's for 'e's and '@'s for 'a's etc. 
## Parameter Prepend
Provide a string you would like prepended to the password output
## Parameter Append
Provide a string you would like appended to the password output
## Parameter Delimiter
This parameter accepts any string you would prefer as a delimiter between words. Defaults to a space.
## Parameter IncludeNumber
Switch parameter to randomly include a number within the passphrase
## Parameter IncludeSymbol
Switch parameter to randomly include a symbol within the passphrase
## Parameter Shortcut
A switch parameter to be used if calling this script from a shortcut link. The Target in the shortcut would look like this if the shortcut was in the same directory as this script:
powershell.exe -noprofile -exec b -command "& {Clear; .\Get-NaturalLanguagePassword.ps1 -pairs 3 -Count 20 -Shortcut}"

This will cause the script to leave the window open for the user to copy/paste the password. Then they can press 'Enter' and the window will close.
## Example  
One of the ways I use this script is to generate a couple dozen passphrases and then I'll select one that I think is more memorable.
```
PS$> .\New-NaturalLanguagePassword.ps1 -TitleCase -IncludeNumber -Count 20
Convex 2Distaste Glib Gong
Candid7 Dawdler Shorter Fib
Sage Gene 6Old Activists
Verdant Ghoul 2Useful Minimum
8Plastic Character Elite Soybean
Poor 3Preplan Correct Drives
Formal Sanctum Glossy 3Climber
Jovial 3Chant Homeless Expanse
Sudsy 0Wall Gloomy Taste
Dyed Humility4 Vast Pulp
Easy Smut Rinsing Parody4
Rusted Motel4 Fabric Rite
Wicked1 Fools Gray Winnings
Wanted Icon Last Upstairs3
6Wavy Gait Maimed Hedge
Whole Load 3Low Obscenity
Surly System High 6Snares
Brisk Flower Chaste0 Molds
Thin Hail Icky4 Shortcut
2Sulky Antlers Artsy Hill
```

If you're really big on character substitution you can add that and maybe just do one pair for something random and memorable.
```
PS$> .\New-NaturalLanguagePassword.ps1 -Pairs 1 -Substitution
$h@ll0w d0lph1n
r3fr13d d1$pl@y
r0gu3 wh1z
h@1ry p0ng
l00ny cr0wd
```
If you'd prefer your own delimiter that can be defined as well
```
PS$> .\New-NaturalLanguagePassword.ps1 -pairs 2 -Prepend "START" -Append "END" -Delimiter '/'
START/chic/rift/busy/platypus/END
```
Knowing that not everyone lives on the CLI I included a `-Shortcut` parameter that alters the output behavior a bit.  
Make a Windows shortcut with a Target similar to this:
```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -noprofile -exec b -command "& {Clear; .\New-NaturalLanguagePassword.ps1 -Pairs 2 -TitleCase -IncludeNumber -Count 10 -Shortcut}"
```  
Or whatever your preferences are for generation.  The shortcut properties could look something like this:  
![ShortCutDetails](/Assets/Shortcut_Details.png)  
Double-click the shortcut and you'll be presented with a window like this where you can copy out whichever candidate phrases you prefer the look of.  
![ShortcutOutput](/Assets/Shortcut.png)
