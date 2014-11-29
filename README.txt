--- OVER VIEW --- (in comments as well)

/*
 * RECURSIVE DUBLOON DECOMPOSITION ALGORITHM.
 * 
 * Background:
 * In Neopets, dubloons are currency used on Krawk island.
 * Dubloons can be bought for NeoPoints, the main currency of Neopets.
 * Dubloons are available in denominations of 1, 2, 5, 10, 20, 50, 100, 200, 500, and 1000.
 * You can combine smaller denominations into higher ones. However, this is generally not worth it.
 * 
 * For example, a one-dubloon coin costs 600 neopoints, and a two-dubloon coin costs 900 neopoints.
 * If we were to combine two one-dubloon coins into a two-dubloon coin, we would be spending 1200 neopoints and only making 900, thus resulting in a loss of 300 neopoints.
 * This is true for all dubloons.
 * The prices of dubloons as of today are as follows:
 * 
 * One-Dubloon Coin: 600np
 * Two-Dubloon Coin: 900np
 * Five-Dubloon Coin: 2500np
 * Ten-Dubloon Coin: 3100np
 * Twenty-Dubloon Coin: 6100np
 * Fifty-Dubloon Coin: 15100np
 * One Hundred Dubloon Coin: 32000np
 * Two Hundred Dubloon Coin: 100,000 np
 * Five Hundred Dubloon Coin: 225,000 np
 * One Thousand Dubloon Coin: 400,000 np
 * 
 * Unfortunately, going backwards (from higher to lower denominations) is impossible - i.e., we cannot break a two-dubloon coin down into two one-dubloon coin.
 * However, we CAN spend ONE dubloon with a 10-dubloon coin in our inventory, and get CHANGE: 
 * 
 * ONE five-dubloon coin
 * TWO two-dubloon coins
 * 
 * In this manner, we can profit, at the sacrifice of ONE dubloon per break-down.
 * 
 * If we spend 3100 np on a ten-dubloon coin, and break it down into two 2-dubloon coins and one 5-dubloon coin,
 * we can sell those for (900 * 2) + (2500) = 4300, netting a profit of 1200 neopoints per ten-dubloon coin bought.
 * 
 * Similarly, a twenty-dubloon coin can be broken down into two 2-dubloon coins, a 5-dubloon coin, and a 10-dubloon coin,
 * and then the process can be repeated for the 10-dubloon coin.
 * 
 * A fifty-dubloon coin can be broken down into two 2-dubloon coins, a 5-dubloon coin, and two 20-dubloon coins,
 * and then the process can be repeated for the 20-dubloon coins.
 * 
 * A onehundred dubloon cn can be broken down into two 2-dubloon coins, a 5-dubloon coin, two 20-dubloon coins, and a 50-dubloon coin,
 * and then the process can be repeated for the 20-dubloon coins and the 50-dubloon coin.
 * 
 * And etc. Thus, a recursive definition is implied.
 * 
 * ---
 * 
 * Algorithm DubloonDecompose(String s, int x, int y, int z):
 * input: 
 * 		1) s, a string denoting the type of dubloon we're decomposing
 * 		2) x, the value of that dubloon we're decomposing
 * 		3) y, the value of a two-dubloon coin at this time
 * 		4) z, the value of a five-dubloon coin at this time
 * output: 
 * 		1) t, the number of two-dubloon coins we can decompose into
 *  	2) f, the number of five-dubloon coins we can decompose into
 *  	3) p, the expected profit, calculated by [t*y + f*z - x]
 *  												(subtract the value of the input dubloon from the # of 2-dubloon coins times its value and the # of 5-dubloon coins times its value.
 * initial bindings:
 * t <- 0
 * f <- 0
 * 
 * RecursiveDecomposition(s)
 * 
 * p <- (x - t*y - f*z)
 * 
 * print: t, f, p.
 *  
 * end
 * 
 * ---
 * 
 * Algorithm RecursiveDecomposition(String s)
 *  (t and f will be global variables so we can modify it from this helper function. this is ok because they are initialized to 0 in DubloonDecompose())
 *  
 *  BASE CASE: 
 *  		if s == "ten",
 *  			t <- t + 2
 *  			f <- f + 1
 *  if (s == "one" or s == "two" or s == "five")
 *  	--> can only decompose 10-dubloon coins or higher
 *  
 *  RECURSIVE CASE:
 *  		else if s == "twenty"
 *  			t <- t + 2
 *  			f <- f + 1
 *  			RecursiveDecomposition("ten")
 *  		else if s == "fifty"
 *  			t <- t + 2
 *  			f <- f + 1
 *  			RecursiveDecomposition("twenty")
 *  			RecursiveDecomposition("twenty")
 *  		else if s == "onehundred"
 *  			t <- t + 2
 *  			f <- f + 1
 *  			RecursiveDecompose("fifty")
 *  			RecursiveDecompose("twenty")
 *  			RecursiveDecompose("twenty")
 *  		else if s == "twohundred"
 *  			t <- t + 2
 *  			f <- f + 1
 *  			RecursiveDecompose("onehundred")
 *  			RecursiveDecompose("fifty")
 *  			RecursiveDecompose("twenty")
 *  			RecursiveDecompose("twenty")
 *  		else if s == "fivehundred"
 *  			t <- t + 2
 *  			f <- f + 1
 *  			RecursiveDecompose("twohundred")
 *  			RecursiveDecompose("twohundred")
 *  			RecursiveDecompose("fifty")
 *  			RecursiveDecompose("twenty")
 *  			RecursiveDecompose("twenty")
 *  		else if s == "onethousand"
 *  			t <- t + 2
 *  			f <- f + 1
 *  			RecursiveDecompose("fivehundred")
 *  			RecursiveDecompose("twohundred")
 *  			RecursiveDecompose("twohundred")
 *  			RecursiveDecompose("fifty")
 *  			RecursiveDecompose("twenty")
 *  			RecursiveDecompose("twenty")
 *  		else
 *  			invalid input
 *  
 *  
 *  Possible closed form:
 *  if n is the denomination of the dubloon, n \in {10, 20, 50, 100, 200, 500, 1000}, ex: n-dubloon coin,
 *  then the number of two's and twenties is
 *  twos: n/5
 *  fives: n/10
 *  
 *  will verify this closed form equation in testing.
 *  Edit: Looks like this closed-form equation is correct for all denominations possible!
 */


