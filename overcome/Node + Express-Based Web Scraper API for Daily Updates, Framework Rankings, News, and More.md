
# Node + Express-Based Web Scraper API for Daily Updates, Framework Rankings, News, and More

This article introduces a **Node.js + Express** project, featuring a versatile web scraper API capable of fetching data from various sources, including daily front-end updates, top framework rankings, news headlines, jokes, and multimedia content.

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Project Overview

### Requirements

- **Node.js**
- **Express**

### Installation and Startup

Clone the repository and install the dependencies:

```bash
$ git clone https://github.com/ecitlm/SpliderApi.git
$ npm install
$ node app.js
```

The server runs on port `3000` by default, and the API endpoints will be accessible immediately after startup.

---

## API Endpoints

### 1. Front-End Development Daily Updates

Retrieve the latest front-end development articles, recommendations, and daily lists.

#### **1.1 Daily Updates List (Last 10 Days)**

- **Endpoint**: `/daily_list`
- **Example**: `http://localhost:3000/daily_list`

#### **1.2 Content Recommendations**

- **Endpoint**: `/recommend_list`
- **Example**: `http://localhost:3000/recommend_list`

#### **1.3 Single Day Report**

- **Required Parameter**: `date` (Format: YYYYMMDD)
- **Endpoint**: `/one_day_list`
- **Example**: `http://localhost:3000/one_day_list?date=20220101`

#### **1.4 Juejin Hot Articles**

- **Endpoint**: `/juejin`
- **Example**: `http://localhost:3000/juejin`

---

### 2. Framework Rankings

#### **2.1 Top 20 Framework Rankings**

- **Endpoint**: `/web_frame`
- **Example**: `http://localhost:3000/web_frame`

---

### 3. Zhihu Daily Articles

Fetch daily articles and details from **Zhihu**.

#### **3.1 Zhihu Daily Data**

- **Endpoint**: `/zhihu_news`
- **Example**: `http://localhost:3000/zhihu_news`

#### **3.2 Article Details**

- **Required Parameter**: `id` (Article ID)
- **Endpoint**: `/zhihu_news_detail`
- **Example**: `http://localhost:3000/zhihu_news_detail?id=1234567`

---

### 4. News Headlines

Fetch categorized news articles and details.

#### **4.1 News List**

- **Required Parameter**: `type` (0: Hot, 1: Society, 2: Entertainment, etc.)
- **Endpoint**: `/news_list`
- **Example**: `http://localhost:3000/news_list?type=0`

#### **4.2 News Details**

- **Required Parameter**: `item_id`
- **Endpoint**: `/news_detail`
- **Example**: `http://localhost:3000/news_detail?item_id=64246032347483345941`

---

### 5. Jokes and Funny Content

#### **5.1 Text-Based Jokes**

- **Endpoint**: `/joke`
- **Example**: `http://localhost:3000/joke`

#### **5.2 Funny Images**

- **Endpoint**: `/joke_pic`
- **Example**: `http://localhost:3000/joke_pic`

---

### 6. Multimedia Content

#### **6.1 Video Content**

- **Required Parameters**: `type` (0: Comedy, 1: Beauty, etc.), `page`
- **Endpoint**: `/video_list`
- **Example**: `http://localhost:3000/video_list?type=0&page=10`

---

### 7. Music Data

Fetch data from **Kugou Music**.

#### **7.1 New Songs**

- **Endpoint**: `/new_songs`
- **Example**: `http://localhost:3000/new_songs`

#### **7.2 Music Details**

- **Required Parameter**: `hash`
- **Endpoint**: `/song_info`
- **Example**: `http://localhost:3000/song_info?hash=123456`

#### **7.3 Music Rankings**

- **Endpoint**: `/rank_list`
- **Example**: `http://localhost:3000/rank_list`

---

### 8. Weather Forecast

Fetch real-time weather information for cities.

#### **8.1 Weather Data**

- **Required Parameter**: `location` (City Name)
- **Endpoint**: `/weather`
- **Example**: `http://localhost:3000/weather?location=Shenzhen`

---

## Conclusion

This project offers a variety of scraping APIs, enabling developers to access data across domains such as front-end development, news, music, and multimedia. With simple installation and robust endpoints, it serves as a flexible solution for data aggregation.

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)
