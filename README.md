# Project2-SIREN-Kraken-RoboTradeAssistant
# Meet Siren
<img src="/image/1.png" width="800" height="400" align=" center">

### **About Siren**
Siren, Kraken RoboTradeAssistant, a right hand tool for a new Kraken user to navigate the basics of the platform such as buying, selling, staking and fetching current market prices through a simple, user-friendly interactive chat. Siren is unlike other “chatbots”, she is a Robo-Trade-Assistant, a sophisticated bot, who is able to execute trades, fetch market prices and stake coins all through an engaging, personal interaction. Once the user has passed the Kraken authentication and validation process, a (new user needing assistance) signal dispatches Siren. The chat icon pops up and Siren waits for the user to verbally state or type in a key word or phrase, triggering the interaction leading to the execution of the user's request.  

The details and functionality of Siren and her workflow are as follows: We created Siren combining AWS Lex and AWS Lambda function. AWS Lex is a service for building conversational interfaces into any application using voice and text. AWS Lex allows you, as a developer, to build bots to increase contact center productivity, automate tasks, and drive operational efficiencies across the enterprise. The key benefits to AWS Lex are simplicity and democratized deep learning technologies. Amazon Lex allows you to create your own basic chatbot in minutes. 

### **The Future is Automation and Rise of Chatbots**
The development of disruptive technologies that reduce or eliminate human intervention in processes has been multiplying exponentially. The effects of such disruptive processes have created a new market that relies upon automated systems rather than human judgement to create near instantaneous and accurate input. The advantage of automation means higher efficiency, including improved production rates and increased productivity, with quicker response time and substantial reduction in overall costs. Chatbots are a perfect example of automation. Browsing the Internet today, chances are, you have had repeated interactions with a chatbot. Chatbots are essentially conversational programs offering customers a more personalized way to access information about a product or service, answer questions, offer options, etc. Their service comes in handy especially for the less tech savvy set, who are navigating challenging environments such as crypto spaces. 

ChatBot = perfect example of Automation. Here are some interesting statistics:
*	25% of mundane and repetitive jobs are at risk of automation
*	375 million jobs are expected to vanish by 2030
*	Artificial intelligence will displace 40% of jobs worldwide in the next 15 years
* Artificial intelligence generated over 2.3 million jobs in 2020 
*	1.4 billion people use messaging apps and are willing to talk to chatbots
*	Chatbots saw a 92% use increase since 2019, making it the brand communication channel with the largest growth 
*	Users have a growing willingness to engage with chatbots in a variety of ways, with usage for purchases, meeting scheduling and mail list sign-ups more than doubling from 2019 to 2020
*	87.2% of consumers rate their typical chatbot experience as within the range of neutral to positive

### **Amazon Lex**
acts as the engine that provides the advanced deep learning functionalities of automatic speech recognition (ASR) for converting speech to text, and natural language understanding (NLU) to recognize the intent of the text, to enable you to build applications with highly engaging user experiences and lifelike conversational interactions, Siren, our Lex bot performs automated tasks through Automatic Speech Recognition (ASR) and Natural Language Understanding (NLU) capabilities.

<img src="/image/2.png" width="800" height="400" align=" center">

### **AWS Lambda**
is a serverless compute service that lets you run code without provisioning or managing servers, creating workload-aware cluster scaling logic, maintaining event integrations, or managing runtimes. With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. In the conversation context, we selected Lambda fulfillment. Amazon Lex invokes the Lambda function  to fulfill the user request after the bot successfully collects all of the required information and receives confirmation from the user. The Amazon Lex bot invokes a custom coded Lambda function synchronously. The event parameter contains information about the bot and the value of each slot in the dialog. The invocationSource  parameter indicates whether the Lambda function should validate the inputs (DialogCodeHook) or fulfill the intent (FulfillmentCodeHook). Amazon Lex expects a response from a Lambda function in the following format. The dialogAction field is required. The sessionAttributes and the recentIntentSummaryView fields are optional. When communication starts with a bot, Lex passes control to the Lambda function we have defined while coding the bot. An event is a JSON variable containing all details regarding a bot conversation. 

```python
def Buy_Order(intent_request):
    """
    Performs dialog management and fulfillment for buying order.
    """
    buy_coin = get_slots(intent_request)["BuyCoin"]
    quantity_buy = get_slots(intent_request)["QuantityBuy"]
    buy_order_type = get_slots(intent_request)["BuyOrderType"]
    buy_order_funding = get_slots(intent_request)["BuyOrderFunding"]
    order_price = 0
    if buy_order_funding == "ETH":
        pair = (buy_coin + buy_order_funding).lower()
        order_price = price_eth(pair)
        total_cost = round(float(quantity_buy) * float(order_price) * 1.0026,8)
    elif buy_order_funding == "XBT":
        pair = (buy_coin + buy_order_funding).lower()
        order_price = price_xbt(pair)
        total_cost = round(float(quantity_buy) * float(order_price) * 1.0026,8)
    else:
        pair = (buy_coin + buy_order_funding).lower()
        order_price = price_usd(pair)
        total_cost = round(float(quantity_buy) * float(order_price) * 1.0026,2)
    return close(
        intent_request["sessionAttributes"],
        "Fulfilled",
        {
            "contentType": "PlainText",
            "content": """Great news, your buy order has been filled for {} {} for a total amount {} {}!
            """.format(
                 quantity_buy, buy_coin, buy_order_funding, total_cost
            ),
        },
    )
```

### **Future Projections**
Projecting forward, Siren prototype can be extended much further by additionally implementing NLP and machine learning. Without NLP, Siren is limited as she relies majorly on pre-fed static information and is naturally less equipped to handle human languages that have variations in emotions, intent, and sentiments to express each specific query. Injecting NLP and machine learning into Siren NLP can pave the way for an easier-to-use interface to features and outstanding services. But more importantly, it will give her users an experience as if they’re having a real conversation, as opposed to going through a limited set of options and menus to reach their end goal. Thus, ideally, the future development for Siren is to continue learning, collecting and storing data, adapting and evolving to the user’s needs and market conditions.

The first leveling up of Siren is to execute complex trades with stop loss and take profit orders. This is a critical first approach as this reduces client risk exposure by setting percentages of risked loss/reward ratios. Next, Siren will be able to interact out of Kraken and into DeFi protocols such as Uniswap and Polkadex. Siren’s will utilize this tactical approach to seek not only more options in Alt Coins, but also decide on which exchange to execute a trade based on the lowest exchange rates. This further gives Siren the option to utilize arbitrage between exchanges and time zones if the opportunity occurs to a guaranteed profit. Through this process, Siren will collect data on trading patterns and trends. As Siren learns and as technology expands, Siren will evolve into an AI trading-assistant bot integrated into numerous exchange platforms for both business and client subscription services. As Siren continues learning and evolving, she will also be able to identify the type of current market sentiments (i.e. bull, bear, or wave market) to base her trades from. This has been a common problem in trading bots as they are coded for one specific form of market, but with machine learning, Siren can adapt to changes in market conditions and volatility. The key note is that Siren cannot predict the news and will be susceptible to such volatilities by executing trades on rash consumer decisions. However, we believe that any trader whether human or bot are all equally vulnerable to such conditions. Siren will have to learn and adjust to the pace of extreme volatility and control her trades based on such.  

## Resources
- [Kraken.com](https://www.kraken.com/en-us/)
- [https://docs.aws.amazon.com/lex/](https://docs.aws.amazon.com/lex/)
- [https://docs.aws.amazon.com/lambda/](https://docs.aws.amazon.com/lambda/)
- [britannica.com](https://www.britannica.com/technology/automation/Advantages-and-disadvantages-of-automation)
- [capacity.com](https://capacity.com/chatbots/faqs/what-is-chatbot-automation/)

<img src="/Image/BuyOrder.gif" width="400" height="600" align=" center"> 
<img src="/Image/sellOrder.gif" width="400" height="600" align=" center"> 
<img src="/Image/stake.gif" width="400" height="600" align=" center"> 
<img src="/Image/FetchPrice.gif" width="400" height="600" align=" center">
