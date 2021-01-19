# LEFT, RIGHT, LENGTH

- In the `accounts` table, there is a column holding the **website** for each company. The last three digits specify what type of web address they are using. A list of extensions (and pricing) is provided [here](https://iwantmyname.com/domains). Pull these extensions and provide how many of each website type exist in the `accounts` table.

```javascript
SELECT RIGHT(website, 3) AS domain, 
       COUNT(*) num_companies
FROM accounts
GROUP BY 1
ORDER BY 2 DESC;
```

- There is much debate about how much the name (or even the first letter of a company name) matters. Use the `accounts` table to pull the first letter of each company name to see the distribution of company names that begin with each letter (or number).

```javascript
SELECT LEFT(UPPER(name), 1) AS first_letter, 
       COUNT(*) num_companies
FROM accounts
GROUP BY 1
ORDER BY 2 DESC;
```

- Use the `accounts` table and a **CASE** statement to create two groups: one group of company names that start with a number and a second group of those company names that start with a letter. What proportion of company names start with a letter?

There are 350 company names that start with a letter and 1 that starts with a number. This gives a ratio of 350/351 that are company names that start with a letter or 99.7%.

```javascript
SELECT SUM(num) nums, 
       SUM(letter) letters
FROM (SELECT name, CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9') 
                       THEN 1 ELSE 0 END AS num, 
         CASE WHEN LEFT(UPPER(name), 1) IN ('0','1','2','3','4','5','6','7','8','9') 
                       THEN 0 ELSE 1 END AS letter
      FROM accounts) t1;
```

- Consider vowels as **a, e, i, o, and u**. What proportion of company names start with a vowel, and what percent start with anything else?