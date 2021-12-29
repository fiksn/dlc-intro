# DLC - a story about betting and self-driving robots

### Characters

We have *Alice* and *Bob* who want to bet against each other regarding what the weather will be tomorrow. Then there is *Olivia* who is working
at a local radio station. She plays music on the radio and announces the weather. So on a given day she might say "if tomorrow is sunny I will play a rock song at 9:00 and in case it rains I will play a pop song". Alice and Bob both listen to that radio station, so they can use it (and Olivia) as an oracle. They need somebody to decide on the outcome since Alice abd Bob might not come to an agreement among themselves (Bob could always claim that is was raining, despite in reality it was sunny).

### Escrow

But first let's look at the finance part. Alice and Bob open a joint bank account. The trick is that withdrawals work just with a statement that is signed by both of them. Alice can come to the bank by herself but she needs a note that is signed also by Bob to get any money.

Additionally there are no overdrafts. If both Alice and Bob have a signed letter that they are able to claim all money, there is a first-come-first-served rule. Letters might also include a time clause like "give Bob 10 EUR but only after 1.1.2021". So if Bob comes with such a letter bank clark will tell him to sit down and wait. During that time Alice can come with a letter that has an earlier restriction date (or none) and empty the account - all while Bob is waiting in the lobby. Of course Bob must have signed Alice's letter some time ago.

Escrow for instance means both Alice and Bob deposit X EUR onto this bank account. And the winner will be able to claim 2X EUR.

### Adaptor signatures

Perhaps you thought such a bank account is weird. But here comes the science-fiction part. Alice and Bob also own special self-driving robots AS1 and AS2. The robots are affiliated with the radio station so beside autonomous driving and stealth mode they have another super power. They can call the radio station, authenticate and get what rock and pop song is scheduled for tomorrow at 9:00. There is no side-channel so there is no way to get this information out of the robot. It is also not possible to impersonate the robot in order to get that data on your own. 

What the robot can do is download the song and drive as long as it is playing. But it will do so only when nobody is watching (since looking at the robot while driving is a very obvious side-channel that could leak the song).

### Contracts

Alice and Bob prepare the bank withdrawal letters. Say Alice bets on "sun" and Bob on "rain".

"Alice can withdraw 2X EUR" will be the "sun contract", "Bob can withdraw 2X EUR" will be the "rain contract". Each contract is printed
twice (that is number of outcomes * 2). The winning party (Alice for the "sun contract") immediately signs it but Bob will sign it only if the contract gets immediately securely stored inside Alice's AS1 robot. On Bob's side it is opposite, Alice is happy to sign "Alice can withdraw 2X EUR", but for "Bob can withdraw 2X EUR" she will also insist on secure storage in AS2.

So in the end Alice's AS1 will store both contracts and Bob's AS2 will store the same two contracts. Same as with the songs there is no way to get the letters out of the robots. Upon tampering the robot will self-destruct.

Additionally Alice and Bob also create and sign a pair of "abort letters" that say "after two days Bob can withdraw X EUR" and similarly "after two days Alice can withdraw X EUR". Remember, if the bank account is empty by then the letter is worthless.

### Hidding the contracts

At night Alice drives to a private place and leaves AS1 there. When Alice disappears AS1 will download the songs for tomorrow. First the rock song. As long as it is playing it will keep driving. That software was audited by Alice and Bob so there is no cheating here. After the music stops the robot will stop, dig a hole and hide the "sun contract" (Alice gets money signed by both Alice and Bob) inside. Then the robot can simply replay the song and drive in the opposite direction to find the starting position. Now it can repeat the process with the pop song (and hide the second letter). After it is done with all of them it will safely drive home.

Bob's robot AS2 will do exactly the same except that Bob drives it to his preferred hidden spot in the park.

The end result will be 4 hidden contracts (2 pairs) in a giant park. Nobody will have the slightest clue where any of those letters is.
Sure Alice and Bob have some starting position where to search but there are still way too many places to find the contracts through brute-force.

### Reveal

Next day at 09:00 the sun is shining so the radio plays "Bohemian Rhapsody". After the song is known Alice and Bob can simply go to their secret starting place in the park and find the hidden "sun conctract" (since they now know the exact length of the song). Bob could dig out his version but as he lost he might not want to cooperate anymore. There is no way for him to find the "rain contract". Also if Bob doesn't dig out his contract Alice will be more than happy to do so with her version and claim the money. Infact she has to do that as soon as possible since after two days Bob could use the "abort letter" to frauduently get his stake back.

### What can go wrong

Bob could collude with Olivia. And at 9:00 we might hear some pop song despite a sunny weather. In that case Bob would indeed get the money this time, but nobody would ever trust Olivia. Afterall there were thousands of people that heard her promise yesterday. They don't know about the specific bet between Alice and Bob (unless somebody explicitly told her) but still everybody knows Olivia is not reliable. (Note that with Olivia having no clue about the bet there is also less possibility that somebody will influence her, but on the down side she also doesnt't get any compensation for playing "judge" except her salary). But this can be abstracted with a market place: it doesn't matter whether you listen to the radio station or not, you still have to pay a "radio subscription fee".

Olivia might play the pop and rock song at the same time in order to help both sides. But in this case it will be just a strange noise and Olivia will lose her job for playing junk (which is even worse than the first option). To apply for the next job she will have to rename herself to Olga.

The third possibility is Olivia just doesn't play any song. Or as it is partly cloudly she plays some rap music. Again the listeners can judge her, but this time they might give her the benefit of doubt. Neither Bob nor Alice can claim victory. Luckily they have their "abort letters" or else without further cooperation between them their funds could be lost at the bank forever. Now they just need to wait another day.
