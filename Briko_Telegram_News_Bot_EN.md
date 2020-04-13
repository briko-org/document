# The COVID-19 News Bot on Telegram
----------
## Open source repo
* Telegram Bot https://github.com/briko-org/brikobot
* Translation Service https://github.com/briko-org/BrikoTranslationService

## Why do we make this COVID-19 news bot?
People all around the world started to focus on the COVID-19 every it was declared as a global pandemic by WHO. In addition to crawling social networks for all the related local news, we also have this urge of trying to find out how other countries are doing despite the language barrier. 

How did the Korean implement their drive-thru coronavirus testing sites in 2 days? What did the Japanese do to keep upcoming Olympic games running? Are there really no increased confirmed cases in China right now? -- It is hard to seek for the news and messages related to this specific topic on a real-time basis, especially when you do not understand the languages.

It is for this purpose, We make this COVID-19 news bot. It will translate the news headlines and SNS messages to your language, so you can be kept up to date with the news about what is going on in the world. You can either subscribe to our channel or become a contributor to this bot.

## How does this COVID-19 news bot work?

![](./Telegram_bot_1.png)

* We have a Telegram channel (https://t.me/briko4covid19) publishing the latest news and valuable social media posts about COVID-19, with a bot translating them into different languages.

* A group of volunteers from different language/cultural backgrounds cooperate to provide news headlines and SNS messages to the bot.

* The bot translates the original texts received and translates them into different languages for publishing in the Telegram channel automatically. 

* By subscribing to the Telegram channel, all users can receive the news updates and will get a prompt after each pushed message, to rate the quality of the translation to improve the translation.

* The suggestions of improvement can eventually be used to train a better machine learning model that would provide more accurate translations.

* Anyone can volunteer to join our contribution team and help collect valuable and interesting posts or news headlines for the bot, and get them translated before pushing to the channel.


## Why do translations look bad on this bot and how to help improve it?

Simply because we lack the source of language corpora: when our bot had never learned what “coronavirus” means in other languages (well, most people including us just learned about it in the past few months), it could not have translated the term correctly. Healthcare-related corpora are greatly needed this task, while most of the resources have been controlled by the tech giants.

If more text corpora in different languages were available, the translation bot would be able to do a better job in translation. Whether you just subscribed to the channel or decided to join our contribution team, you could help make this bot better or even an expert in the translation of this particular area. 

![](./Telegram_bot_2.png)

A click on the score indicating the quality of the translation, if you knew both of the languages, would greatly help our bot!

What do we give back to the community?
Everything! We do not take away any of the works done by the community and hide them for ourselves. In contrast, we will open-source everything we have as well as everything the community contributes to this bot, our plan includes but is not limited to the following:

* Source code of the Telegram bot itself,
* Text corpora of languages we support,
* Source code processing the above text corpora,
* Machine learning model we made using the text corpora,
* Users contributed improvement to translated news and messages.

We hope by doing this work in a completely transparent manner, everyone can benefit from some parts of this project. 

Learn about the latest coronavirus news and messages on SNS, start learning a foreign language by reading, take a try on machine learning translation models, or try to make your own Telegram bot, no matter what your interests are of this project, you are welcome to join us!





