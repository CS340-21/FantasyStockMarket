# Merchant Sim 1434

## Computer Pub:

* Andrew Banks

* Austin Rhodes

* Dylan Sullenberger

* Holland Johnson

* Joshua Byers

## Section 1: Introduction

Merchant Sim 1434 is an incremental/idle game that blends classic clicker-style progression with a simulated market. Though plenty of incremental/idle games have been done before, ours has the unique angle of allowing the player to trade their earned rewards in a simulated market that takes inspiration from real world stock trading. Our team collectively has an interest in gaming and a curiosity of game development, and is eager to try our hand at it using the software design process. We’re defining ‘incremental/idle game’ as a genre in which players are presented with passive, simple decisions that incrementally progress the gameplay. In our case, players begin with a small amount of money and earning potential and through passive and simple interactions are able to grow their worth and spend this money to unlock new features. The simulated market serves to multiply the player’s earned capital, allowing the player to invest and speculate, eventually attaining digital exuberance. The final result of this project was a functional web based game that included all of the intended basic functions. All of the basic project goals were met, however there were some additional features that were not able to be implemented, such as a guild system, market manipulation, and future predictions.

## Section 2: Customer Values

The primary customer for Merchant Sim 1434 is the general public (whoever wants to play our game), and our customers seek entertainment. While their underlying problem to be solved is boredom, our customers also want to experience a fantasy world with quests and invest in a market without any real risks. Our software in the context of the real world market shows that our game stands out from other idle games because of its unique market element. From the customer's point-of-view, our solution will solve the customers' boredom and allow customers to invest in the market with no real world monetary liabilities. The customer will also benefit from our proposed solution as they will no longer be bored and will instead be entertained. Additionally, our game provides a unique experience by introducing the player to a stock market in a fantasy setting. We have already tested the idea on at least one person, and they were interested. We could know if customers got the benefits we want to provide by creating a feedback system or asking for reviews of our game. Our customer-centric measures of success are five star reviews.

No changes.

## Section 3: Technology

### 3.1 Environment

The game is played in browser, with the entire game logic running client side within JavaScript. Though the demo currently runs off of Github Pages, it's possible to run the game on any standard web server, and in any web browser.

### 3.1 Design 

In order to simulate a market that the player can interact with and make meaningful choices in, we wanted a way to control the prices of items but not so directly that it made the game feel static or predictable. The solution was to implement a loosely manipulable price fluctuation algorithm with a set of parameters that we could adjust from our other gameplay systems. The price fluctuation algorithm governs the general prices and 'shape' of price movements over time, but doesn't explicitly set prices which makes the market feel realistic and alive. Other gameplay systems, like quests or random events, can simply adjust these parameters to achieve a desired price movement. This system has the huge advantage of allowing new content or systems to be added to the game without having to rewrite or reinvent much code.

The other gameplay systems besides this underlying framework are the quests, random events, and monarchy system:

Quests are player interactions that change the status of the market directly. e.g. the player clicks the 'manipulate wine prices' quest which causes an immediate change in the wine prices.

Random events occur every few iterations of the game loop and also immediately change the status of the market, however are not voluntary and occur without player interaction. e.g. the price of scrolls has fallen today.

The monarchy acts as a kind of major, more predictable event for the player to pay attention to. Monarchs in power have a permanent effect on the prices of a particular type of item, such as magic items or war items. Every time a monarch dies, a new monarch is selected randomly from a list of candidates, and the list of candidates is repopulated from the pool of possible monarchs. This way the player is able to keep track of who the next monarch may be by viewing the current candidates, but does not know exactly which one will win.

### 3.2 Implementation

The implementation of price fluctuation is simple enough. There is an array of Item objects which represent each purchasable item in the game. Each item contains a 'bias' (the target price to fluctuate around), 'volatility' (maximum daily price shift), and of course the 'price'. The game effectively runs in a while(1) loop, iterating through this array once per second and calling priceShift() on each item to update the prices. priceShift() simply moves the price up or down by a random amount that is not higher than the 'volatility' of the item. If the current price happens to be above (bias + volatility) or below (bias - volatility) (such as if an event has just occurred to move it outside this range) then priceShift() must move the price towards the bias. Otherwise, there is a 50/50 chance that the price will move up or down.

The events system selects a random event from a list every few iterations of the game loop. The events adjust the underlying parameters for a particular item directly, which will effect the price fluctuation algorithm subsequently.

Quests are implemented as functions that are called on button click. This allows quests to do pretty much anything in addition to affecting the underlying parameters, with some quests involving random dice rolls that determine their success chance.

The monarchy system is implemented with a first array, 'kings', containing all possible monarchs. A second array, 'candidates', contains a selection of monarchs who are slated to be the next ruler. When the current monarch dies, a random monarch is selected from the 'candidates' array and 'candidates' is populated with new monarchs from the 'kings' pool. Each time the succession happens, the parameters of all items of the monarch's type (war, magic, etc.) are changed.

### 3.3 Tests

The method of testing used was playing the game. When testing, it's important to pay attention to both the functionality of the program as well as the quality of the game itself. The functionality of the program was readily tested using different browsers and different browser sizes and mainly by trying to manually exhaust all of the features of the game to make sure they work. These functionality tests were used to fine tune the interface to fit other displays and make the game more organized and easier to navigate. 

The quality of the game was tested by trying to play it properly, and this testing proved to be incredibly important as without it many game-breaking inconsistencies wouldn't have come to light. For example, clever manipulation of the systems can result in infinite money exploits (not necessarily glitches) which undermine the gameplay, so care must be taken to account for all possible player strategies so that one doesn't come out dramatically on top of all others. This was unexpectedly challenging to deal with, and a considerable amount of time was spent balancing the gameplay systems out.



## Section 4: Team 

Andrew and Austin were responsible for software development, with Andrew focusing on the event and monarch systems and Austin focusing on the stock and quest systems.  Joshua was also responsible for the software development of the layout with CSS.  Holland was responsible for most of the art.  Dylan was responsible for the writing (specifically of the events), as well as helping out with various aspects of the software development.  All group members contributed about the same.  Team member roles changed from the initial proposal, but once we established the actual roles they remained mostly static.


## Section 5: Project Management 

The team met every Tuesday and Thursday to discuss what needed to be completed for the week. The team also constantly communicated through Discord to ask questions, share ideas, and ask for help. All the following basic goals for the project were met: stock trading, quests, events, and monarchs. There were various other features the team was hoping to add if there was extra time (such as, starting a guild for quests that could be leveled up, providing the ability to become the monarch, creating magical items that can manipulate the market, etc.). There were also some basic concepts that we did not think of until late into the project that were not completed like save systems and stock portfolios. Unfortunately, some time was lost due to an unfamiliarity with JavaScript, interpreted languages, a dynamically changing website, and type coercion. Getting over the GitHub learning curve was especially difficult in order to begin collaborating.

## Section 6: Reflection 

For our project, our stock system went well, as did our event system. Not so well were other features we had planned on adding, such as a system to look into the future, more stock options, and even late-game stuff. For planning, at least on the side of the CSS and HTML, it was pretty light. Just design the basics of the UI and the rest just fell into place. On the javascript side, it was all split up into parts, such as the stock market simulation, the event system, the monarch system, etc.. The development was just each piece being worked on individually by one person, with another person helping out where necessary. Testing was done with tools to see the bias and volatility to see how they changed over time. Overall, the biggest thing to be aware of was not to have one of the stock options go into the negatives or just become completely worthless, which did occur early on.

Overall, I would consider this project a success. Though we weren’t able to add as many features as we wanted, nor did we add as many stock options as had been planned, we were able to get the base systems set up.
