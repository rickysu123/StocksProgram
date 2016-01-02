def readFile():
    # returns a list of lists. Each list inside represents one day
    contents = []
    # reads the file from bottom to top, reversing the original order
    # so it reads the file from oldest stock to newest stock
    for line in reversed(list(open("Apple_stocks.csv"))):
        newLine = line.rstrip().split(",")       # split line by commas
        contents.append(newLine)
    del contents[-1]            # remove the row with column names
    return contents


content = readFile()


def info():
    # gets type of price user wants to average, price to buy/sell against
    # and number of days to average over
    dic = {"open" : 1, "high" : 2, "low" : 3, "close" : 4} 
    averageType = input("Which price would you like to average over?\n\
open, close, high, or low: ")
    priceAgainst = input("Which price would you like to buy and sell against?\
                          \nopen, close, high, or low: ")
    averageDays = eval(input("How many days would you like to average over?: "))
    # returns the index of the price type and 
    # the number of days the user wants to average over
    return dic.get(averageType) , dic.get(priceAgainst), averageDays


def numberInfo(averageDays):
    # percentage of current stocks to sell, pecentage of current stocks to buy
    # ratio difference between buying and selling
    buy_percent = eval(input("What percentage of the maximum amount of \
stocks you are able to purchase, would you be willing to buy?\nPlease enter \
as a decimal: "))
    sell_percent = eval(input("What percentage of your stocks would you \
be willing to sell?\nPlease enter as a decimal: "))
    buy_threshold = eval(input("Based on the average of the past number of \
days you provided, how much lower than that average would you be willing \
to BUY stocks? Please enter as a decimal: "))
    sell_threshold = eval(input("Based on the average of the past number of \
days you provided, how much higher than that average would you be willing \
to SELL stocks? Please enter as a decimal: "))
    return buy_percent, sell_percent, buy_threshold, sell_threshold
    
    
def mean(prices):
    # returns average of a list
    total = 0
    for number in prices:
        total += number
    total /= len(prices)
    return total

def transaction(buy_percent, sell_percent, buy_threshold , sell_threshold, \
                money, stocks, averagePrice, dayPrice):
    buy_price = averagePrice * (1 - buy_threshold)  # set percentages
    sell_price = averagePrice * (1 + sell_threshold)
    if dayPrice <= buy_price:    # buying
        ableToBuy = int(money/dayPrice)     # max number of stocks able to buy
        buying = int(buy_percent * ableToBuy) # percentage of max stocks to buy
        stocks += buying
        price = buying * dayPrice
        money -= price
    elif sell_price <= dayPrice:   # selling
        sell = int(sell_percent * stocks)   # amount to sell
        profit = sell * dayPrice
        money += profit
        stocks -= sell
    return money, stocks

def main(content):
    money = 1000                # keep track of money
    stocks = 0                  # keep track of number of stocks
    priceType, priceAgainst, averageDays = info()
    buy_percent, sell_percent, buy_threshold, sell_threshold =\
                 numberInfo(averageDays)
    # get price type to average over and number of days to average over
    # along with the type of price to buy/sell against
    prices = []                      # list of the average prices
    count = 1                        # keep track of the initial days
    for i, line in enumerate(content):
        if count <= averageDays:
            # get initial prices
            prices.append(eval(line[priceType]))    
            count += 1
            continue
            # get initial prices
        averagePrice = mean(prices)       # get average of prior days
        dayPrice = eval(line[priceAgainst])  # get the priceType of current day
        money, stocks = transaction(buy_percent, sell_percent, buy_threshold\
                                    , sell_threshold, money, stocks,\
                                    averagePrice, dayPrice)
        del prices[0]    # remove the oldest day from prices
        prices.append(eval(line[priceType])) # take new price of current day
    if stocks > 0:
        sellRemain = stocks * dayPrice  # dayPrice is latest price
        money += sellRemain
        stocks = 0
    print("\nYou started with $1000. You now have:")
    print("Money = $%.2f , Stocks = %d" % (round(money,2), stocks))
    

main(content)

if __name__ is "main":
    main()

print("\n\n")


def firstToLastDay(content):
    # this answers the question of: How does your algorithm compare to
    # purchasing as much stock as possible on the first day and selling
    # on the last?
    # will use lowest price on first day and highest price on last day
    print("How does the algorithm compare to purchasing as much stock as \
possible on the first day and selling on the last?\nWe will buy at the low \
price on the first day, and sell all stocks on the high price on the last \
day.\n")
    money = 1000
    stocks = 0
    buyPrice = eval(content[0][3])    # buy at low price on first day
    sellPrice = eval(content[len(content)-1][2])
    # sell at high price on last day
    # buy as many stocks as possible
    stocksToBuy = int(1000/buyPrice) # max amount of stocks able to buy
    money -= stocksToBuy * buyPrice     # subtract from original money
    stocks += stocksToBuy
    print("After first day, at stock price $%.2f: \n \
Money = $%.2f , Stocks = %d" % (round(buyPrice,2), round(money,2), stocks))
    money += sellPrice*stocks
    stocks -= stocksToBuy
    print("After last day, at stock price $%.2f: \n \
Money = $%.2f , Stocks = %d" % (round(sellPrice,2), round(money,2), stocks))

firstToLastDay(content)
print("\n\n")


def stockPriceGrow(content):
    # this answers the question of: Does the stock price grow over time?
    # since the data represents 15 years of stock,
    # I will print 15 of the prices, evenly divided in time,
    # from beginning to the end
    print("Does the stock price increase over time? \nHere are the opening \
prices of the Apple stock, divided evenly into 15 dates, since the stock \
represents 15 years.\n")
    time = int(len(content)/15)
    everyYear = []
    for i in range(0,len(content),time):
        print(content[i][0], "\t$%.2f" % eval(content[i][1]))
    print("\nAs you can see, there was a small dip from the years 2002 to 2003\
. What is interesting is the huge dip from 2007 to 2008. Apple stock prices \
dipped way down to $115.44 on February 26, 2008 then shot back up to $192.24 \
on May 14, 2008 The price then lowered back down to $154.82 on August 5, 2008 \
increased a small amount, and then continued to decrease to $95, fluctuating \
around that price for a couple of months. The stock price then began to \
steadily increase from then on up to $631 in October 2012. The price \
decreased a small amount, then increased back up to the $600+ mark. \
On June 9, 2014, Apple split their stocks. This meant that any shareholders \
would get a certain amount of shares for each of their current shares. This \
multiplied each shareholder's number of stocks, while decreasing the stock \
price so that more people can purchase the stock and trade. This is why the \
price decreased suddenly. From then on, the price increased.\n\n")

stockPriceGrow(content)

def altAlgorithm(content):
    # my own algorithm
    print("Here is my own algorithm.\n")
    print("The method is as follows: purchase as much stock at the beginning \
of the year as possible, and sell all stocks at the beginning of next year. \
When purchasing, purhcase at the close price of the day, and when selling, \
sell at open price of the day.")
    money = 1000                # keep track of money
    stocks = 0                  # keep track of number of stocks
    year = "2001"
    firstYear = True    # for the first year in the for loop
    for i, line in enumerate(content):
        tempYear = line[0].split("-")[0]    # get year of the current date
        if firstYear == True:    # specifically to buy stocks for first year
            firstYear = False   
            buyPrice = eval(line[4])    # buy at close price on first day
            stocksToBuy = int(1000/buyPrice) # max amount of stocks able to buy
            money -= stocksToBuy * buyPrice     
            stocks += stocksToBuy   # add to stocks
        if year != tempYear:    # new year
            year = tempYear     # change year
            sellPrice = eval(line[1])   # sell at open price
            money += sellPrice * stocks
            stocks = 0      # sell all stocks
            # buy back stocks
            buyPrice = eval(line[4])    # buy at close price on first day
            stocksToBuy = int(1000/buyPrice) # max amount of stocks able to buy
            money -= stocksToBuy * buyPrice     # subtract from money
            stocks += stocksToBuy   # add to stocks
    if stocks > 0:      # sell remaining stock when bought on last day
        money += stocks * buyPrice
        stocks = 0
    print("Money = $%.2f , Stocks = %d" % (round(money,2), stocks))
    print()
    print("How does this algorithm compare to the moving average algorithm?")
    print("This algorithm generally makes more money than the moving average, \
most likely because I know that the stock price generally increases over time, \
so buying stock at an earlier time and selling it later creates more profit.")
    
altAlgorithm(content)
