# Basic Anchor RSS feed scrape

Connect and scrape public RSS from https://anchor.fm/. The RSS needs to bet set to public.

I recommend viewing the rss url in browser first to see the structure, below I show how to scrape through some key items

```javascript

const RSS_URL = `YOUR RSS URL HERE`;

fetch(RSS_URL)
  .then(response => response.text())
  .then(xmlString => {
    const parser = new DOMParser();
    const dom = parser.parseFromString(xmlString, 'application/xml');
    return dom;
  })
  .then(dom => {
    let items = dom.querySelectorAll('item');
    
    
    /* loop through key items of  available podcasts */
    for (i = 0; i < items.length; i++) {
      let title = items[i].getElementsByTagName('title');
      let pubDate = items[i].getElementsByTagName('pubDate');
      let summary = items[i].getElementsByTagName('itunes:summary');
      let duration = items[i].getElementsByTagName('itunes:duration');
      let itunesImage = items[i].getElementsByTagName('itunes:image');
      let image = itunesImage[0].getAttribute('href');
      let enclosure = items[i].getElementsByTagName('enclosure');
      let audioUrl = enclosure[0].getAttribute('url');
    }
  });

```
