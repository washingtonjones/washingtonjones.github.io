---
author: Washington Jones
timestamp: 1591288563
---
One thing that you may not know about me, aside from not knowing anything about me, is that I love cryptography. Not necessarily in the data security sense — although I love that as well — but rather in the puzzle solving sense. Every day around noon I like to look up a daily cryptogram, which is typically a quote or a definition enciphered using a simple substitution cipher. I write the cryptogram down and then attempt to solve it while I eat my lunch. Oftentimes this is the highlight of my day, which says almost as much about my love for puzzles as it does for my lack of a life.

There’s something about patterns and pattern-matching that’s truly enrapturing to me, and has been so my entire life. I remember being a child and believing that I could solve any problem in the known universe if I could tie just the right pieces together. My complete lack of impact on society in adulthood, however, proves that I’ve been consistently bad at solving problems — but I digress.

While researching ciphers yesterday, I came across the Solitaire cipher<sup id="ref-1"><a href="#fn-1">1</a></sup>, which Bruce Schneier created for Neal Stephenson's novel "Cryptonomicon." It's a cipher that can be implemented using a standard deck of playing cards, the idea being that a deck of cards is more covert and affordable than computer equipment when living under an oppressive government. I quickly fell in love with this concept, of using an ordinary object to pass someone a secret key with discretion — who would suspect that the deck of cards you handed your friend is really the key to unlock some secret message?

As I was reading about this cipher, I still hadn’t come up with my “make something new” for that day. I decided to try coming up with my own unassuming object cipher, preferably one that’s not as complicated as the Solitaire cipher — something more like a toy cipher that even a child could understand and use. I started looking around the house, and I came across a set of four dice in my closet.

Such a serendipitous find! Cryptographers always talk of the need for true randomness in security, and what everyday object better represents randomness than the roll of a die? In fact, a key generated with a die roll wouldn’t even need to be physically handed to the recipient of a message. I began to imagine someone taking a selfie with their dice in the background, a key hidden in plain sight and understood only by the two people who are communicating with one another. Yes, dice would work perfectly for my new cipher.

This is when I designed the Die cipher version 1.0. You see, in my enthusiasm for creating a new cipher, I’m afraid that I forgot one very important thing: encrypted messages must also be decrypted. You would think such a thing would be fairly obvious to even a casual observer but, unfortunately, I am not a very obvious person. Before I continue further, let me explain how the Die cipher version 1.0 works:

*1*) Put together a set of four six-sided dice, ensuring that one die is a different color than the rest (a requirement that definitely did not arise from the fact that my own dice happened to fit this exact description, definitely).

![A set of four six-sided dice. One die is pink, the rest are white.](/assets/images/2020-06-04-image01.jpg)

2) Roll the dice to generate your encryption key. In the example below, my key is 2-6-1-4.

![The rolled dice landed in the order two, six, one, and four. The first die, which landed on two, is the pink die.](/assets/images/2020-06-04-image02.jpg)

*3*) Take note of the arrangement of the dice where they landed, as the off-color die represents one of four math operations — addition, subtraction, multiplication, and division, as illustrated below.

![The dice are lined up in the same order they landed, each one under a math operation sign — addition, subtraction, mutlipication, and division. The pink die is in the first position, which is addition.](/assets/images/2020-06-04-image03.jpg)

4) Take the message that you want to encrypt and shift each letter a number of letters to the right equal to the number on each die. For example, with the message “HELLO WORLD”, the H would be shifted 2 letters to the right, the E would be shifted 6 letters to the right, the first L would be shifted 1 letter to the right, and the second L would be shifted 4 letters to the right, all resulting in JKMP.

![The first four letters have been shifted, transforming from H E L L to J K M P.](/assets/images/2020-06-04-image04.jpg)

5) For the next letter in the message, cycle back to the beginning of your key and perform a math operation on each number to transform the key. In the below example, the off-color die landed on 2 and is in the addition position, which adds 2 to each number in the key. You can then use these new values to continue shifting the letters in your message. 
  - Note that if any value cause the letters to extend past Z — the 26th letter of the English alphabet — you can use modular arithmetic to wrap back around to the beginning of the alphabet. In the illustration below, W is the 23rd letter of the alphabet and is being shifted by 8 letters, resulting in 31. You can perform modular arithmetic by dividing 31 by 26 and using the remainder (5) to determine which letter W will transform to (E, the 5th letter of the alphabet).

![The four numbers of the original key have all had two added to them, which happens because the pink die landed on two and is in the addition position.](/assets/images/2020-06-04-image05.jpg)

6) From here you would continue to repeat step 5 by performing the math operation on the value from the previous cycle. In the example below, 2 is now added to the previously calculated values of 4-8-3-6 to produce 6-10-5-8. The final two letters are then shifted, and we finish transforming our message “HELLO WORLD” into “JKMPS ERXRN.”

![After two and a half cycles of transformation, the message HELLO WORLD has changed to JKMPS ERXRN.](/assets/images/2020-06-04-image06.jpg)

To be honest, I felt pretty proud of myself after designing that cipher. It’s not secure, of course — an attacker could simply brute force the key by trying every possible combination with every possible math operation. However, given that I intended to create a toy cipher during a 20 minute break, it felt reasonably secure enough given the low-threat model behind its design. It wasn’t until I began describing the cipher to someone later on that I realized it had even more problems than I thought.

For one, I never decided on how to handle division as part of the cipher, as that would always result fractional numbers. I initially put this concern aside with the vague notion of using the number in the tenths decimal position, believing that I could iron out the rough spots later on. Unfortunately, the second problem proved to be the bigger issue, especially in regards to the division conundrum.

Like I said before, my excitement for creating a new cipher caused me to focus solely on encrypting a message — I had completely overlooked decryption. The math used to encrypt a message is simple to perform (although tedious with longer messages) and ends with very different key values from the original dice roll. This means that the recipient of a message has to look at the original key, count the length of the enciphered message, and pre-calculate the ending key values before they can begin decrypting the message. This, of course, puts quick and easy use of the cipher entirely out of reach — an unforgivable sin for a toy cipher to commit!

I decided to scrap the Die cipher version 1.0 and try again, this time focusing less on reasonable security. I wanted to create something that was simple and fun to use, something that perhaps would have been in one of the toy spy kits I had as a child. Die Cipher version 2.0 was much easier to create and took only a few minutes to design. It works as follows:

**1**) Grab a set of dice. Any number of dice will do provided that one die is somehow distinct from the others — a different color, or a different number of sides, etc..

*2*) Roll the dice to generate your encryption key. In the illustration below, the key is 3-6-2-4.

![The dice roll has provided the key values three, six, two, and four.](/assets/images/2020-06-04-image07.jpg)

3) The distinct die is your modifier, and its value should be added to the numbers rolled on each die. In the illustration below, the modifier die’s value is 4, so we add 4 to each number in the key to get 7-10-6-8.

![The pink die is the modifier die and it landed on four, so four gets added to each value in the key.](/assets/images/2020-06-04-image08.jpg)

4) Take the message that you want to encrypt and shift each letter to the right equal to the values in the modified key. Using the “HELLO WORLD” example again, the H would be shifted 7 letters to the right, the E would be shifted 10 letters to the right, the first L would be shifted 6 letters to the right, and the second L would be shifted 8 letters to the right, resulting in “OORT.”

5) When you reach the end of the values in your key, cycle back to the beginning of the key values and repeat step 4. Do this until the entire message is encrypted. Continuing the “HELLO WORLD” example, the O would be shifted 7 letters to the right, the W would be shifted 10 letters to the right, the next O would be shifted 6 letters to the right, and so on. Remember to use modular arithmetic if needed to wrap around to the beginning of the alphabet. Doing so fully transforms “HELLO WORLD” to “OORTV GUZSN.”

![The fully encrypted message changed HELLO WORLD to OORTV GUZSN.](/assets/images/2020-06-04-image09.jpg)

The sharp cryptanalysts out there have likely noticed that this is essentially a slightly modified Vigenère cipher using dice, and they would be essentially slightly correct. As such, it’s subject to the same vulnerabilities as the Vigenère cipher<sup id="ref-2"><a href="#fn-2">2</a></sup>. Still, the Vigenère cipher was considered uncrackable back in its day, which I believe to be sufficient for introducing budding young minds to the world of cryptography in a fun and accessible way. As such, I believe I may be prouder of this much simpler cipher than I was of my original design. Any kind and number of dice will do<sup id="ref-3"><a href="#fn-3">3</a></sup>, with any number of sides allowed — the only requirement is that one die be distinct from the others. For example, you could use a D10 as the modifier die in a set of D6, or mix a die marked with numbers into a set of dice marked with dots. In fact, the cipher is still completely usable even if none of the dice are distinct at all. You could just as easily tell the recipient the position of the modifier die — “it’s the third from the left” or “it’s the one by itself on the other side of my desk.”

I believe I accomplished my goal with this little project: a toy cipher using unassuming objects laying around the house. Apropos of nothing, if anyone is publishing a spy book for children, I might have just the thing for you to include.

---

### Footnotes

I did a quick search before writing this post to see if a dice-related cipher already exists. The closest thing I could find is [this cipher](http://bestcodes.weebly.com/dice-cipher.html) that doesn't use dice but does use similar dice dots to represent English characters.

<a id="fn-1" href="#ref-1">[1]</a> Information regarding the Solitaire cipher can be found on [Bruce Schneier's website](https://www.schneier.com/academic/solitaire/).

<a id="fn-2" href="#ref-2">[2]</a> For example, an attacker can analyze the ciphertext to look for places where the same words happen to be encrypted by the same key numbers in the same order, which causes those words to be repeated in the ciphertext. Such repetitions can provide clues regarding the length of the key, which brings the attacker one step closer to cracking the cipher. This method is known as the “Kasiski examination”, named after Friedrich Kasiski, the one who published a paper detailing its use in 1863. Auguste Kerckhoffs further refined this attack to extract the key itself through analysis of the ciphertext. If you’re interested in learning more about these methods, I recommend [this article from the “Crypto Corner” of interactive-maths.com](https://crypto.interactive-maths.com/kasiski-analysis-breaking-the-code.html).

<a id="fn-3" href="#ref-3">[3]</a> This cipher can technically be performed with a single die, which acts as its own modifier. In practice, this would be similar to using a die to pick a key for the Caesar cipher.

---

```YINO FSPH QR EUCGMLPK VKKW FLG GKSJIT HCWVHT IIJ```