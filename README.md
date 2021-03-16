# Twitternity

Archive tweets from Twitter by writing them to the Ethereum blockchain.

If people want to see tweets you've archived, you can win a lottery powered by Chainlink's verifiably random function.

## Use cases for MVP

### Users can archive tweets.

**Ultimate:** a browser extension that, when clicked, archives the tweet the user is currently viewing. If they aren't viewing a tweet, or are viewing their feed instead of a specific tweet, prompt the user to view a single tweet.

**Probably easier:** a web client with a simple form that lets users enter a link to a tweet to archive it. Submitting the form would 1) fetch the tweet via the Twitter API, then 2) prompt the user to pay for the transaction to write the tweet to the blockchain, and finally 3) show them the archived tweet and prompt them to archive another one.

### Users can view archived tweets.

**Ultimate:** a browser extension that detects deleted tweets on a page, checks to see if we have it archived, and, if we do, renders it where the "This tweet has been deleted" text would otherwise be, with a disclaimer that the tweet had actually been deleted and was being served from the **twitternity** archive.

**Probably easier:** a web client gallery of archived tweets. Searchable by display name, username, or content would be all the better.

### When a user views an archived tweet, we tally it.

Two parts: 1) how to track the view tally of archived tweets without bankrupting Readers, and 2) how to prevent Readers from gaming the system.

Tricky tricky. Brain dump of considerations:

Since the tally is what determines who gets paid what, it's crucial not to hide it. This suggests every tally should be written to the blockchain, but writing to the blockchain is a transaction, and transactions cost ETH. Readers are gonna find far less value in this service if they have to pay every time they want to view an archived tweet.

Could tally off-chain, but then there's the trust issue. Perhaps there's another way to make our off-chain database transparent enough for demo purposes?

Something something Ethereum layer 2 scaling solutions like Optimism. This is probably the best option technically, though almost certainly the most complicated.

Additionally, we can't just count each request to view an archived tweet the same or it's too easy to game the system. Tallies need to be weighted based on the authenticity of the requesting user. I think we can build an algorithm around their account age (how long it's been since they created their Twitter account) as well as the number of followers they have.

### Every week we distribute the fees we've collected to an Archivist.

This is where Chainlink's VRF (verifiably random function) comes in. Wherever we cannot avoid incurring transaction fees, we request a little extra and throw it in Free Parking. Each request tally for an archived tweet is basically a lottery ticket, and every week we select one at random using Chainlink VRF and reward the Archivist who archived that tweet everything in Free Parking.
