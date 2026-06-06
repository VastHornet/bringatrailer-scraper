[Bringatrailer Scraper](https://apify.com/silentflow/bringatrailer-scraper?fpr=data)

**230,000+ completed vehicle auctions with sold prices, specs, and VINs.** Search by make, model, or year. Get structured data from the largest enthusiast car auction platform in seconds.

## How it works

![How Bring a Trailer Scraper works, from search to structured auction data](https://images.apifyusercontent.com/AKNgi8FUXQEV9uD81Cnaj7LvgqwGhEZL_nnBC3mabUo/w:1800/cb:1/aHR0cHM6Ly9hcGkuYXBpZnkuY29tL3YyL2tleS12YWx1ZS1zdG9yZXMvTXNNem1vT0NYcUNWMjNpSDIvcmVjb3Jkcy9ob3ctaXQtd29ya3MtdjIucG5n.webp)

## ✨ Why teams use this scraper

Building a car valuation model but can't get historical auction data? Copy-pasting sold prices from BaT listings one by one? Trying to track what a specific model sells for over time?

- 🚗 **230,000+ completed auctions.** Every sold vehicle on Bring a Trailer with final prices, bid counts, and auction dates. The largest structured dataset of enthusiast car sales available.
- 💰 **Sold prices you can't get anywhere else.** BaT doesn't have a public API. This scraper gives you structured access to every completed auction result.
- 📋 **Full vehicle specs per listing.** VIN, mileage, engine, transmission, exterior color, interior color, and all listed essentials. No manual data entry.
- 📸 **Gallery photos included.** Every listing comes with all gallery image URLs, typically 30-60 photos per vehicle.
- 🔍 **Search by anything.** "Porsche 911", "BMW E30 M3", "1967 Mustang", or browse by model page URL. Get exactly the vehicles you're looking for.
- 👤 **Seller and location data.** Know who sold it and where the vehicle is located.

## 🎯 What you can do with BaT auction data

| Team | What they build |
| --- | --- |
| **Car Dealers** | Price inventory accurately using real auction comps for any make and model |
| **Investors** | Track which models are appreciating and identify undervalued vehicles |
| **Insurance** | Get accurate market values for specialty and collector vehicles |
| **Appraisers** | Support valuations with actual transaction data, not estimates |
| **Data Journalists** | Analyze collector car market trends with structured, exportable data |
| **Enthusiasts** | Track dream car prices and set alerts when deals appear |

## 📥 Input parameters

| Parameter | Type | Description |
| --- | --- | --- |
| `searches` | string[] | Keywords to search (e.g., "Porsche 911", "BMW M3 E30") |
| `startUrls` | URL[] | Direct BaT listing or browse page URLs |
| `maxItems` | integer | Maximum results to return (default: 50) |
| `includeDetails` | boolean | Fetch full specs, VIN, and photos from each listing (default: true) |

## 📊 Output data

```
{
  "title": "1989 Porsche 911 Carrera 4 Coupe",
  "price": 72500,
  "priceFormatted": "USD $72,500",
  "currency": "USD",
  "status": "sold",
  "auctionEndDate": "2026-03-15T22:00:00Z",
  "totalBids": 38,
  "noReserve": true,
  "vin": "WP0AB0969KS450123",
  "mileage": "64,200",
  "engine": "3.6L Flat-6",
  "transmission": "5-Speed Manual",
  "exteriorColor": "Guards Red",
  "interiorColor": "Black Leather",
  "essentials": ["Clean Title", "Service Records", "Recent Service"],
  "seller": "bringthetrailer",
  "location": "San Francisco, CA",
  "imageUrl": "https://bringatrailer.com/wp-content/uploads/...",
  "imageUrls": ["https://...", "https://...", "... 45 photos"],
  "excerpt": "This 1989 Porsche 911 Carrera 4 is finished in Guards Red...",
  "url": "https://bringatrailer.com/listing/1989-porsche-911-carrera-4-38/"
}
```

## 🗂️ Data fields

| Category | Fields |
| --- | --- |
| **Vehicle** | `title`, `vin`, `mileage`, `engine`, `transmission`, `exteriorColor`, `interiorColor`, `essentials` |
| **Auction** | `price`, `priceFormatted`, `currency`, `status`, `auctionEndDate`, `totalBids`, `noReserve` |
| **Seller** | `seller`, `location` |
| **Media** | `imageUrl`, `imageUrls`, `excerpt` |
| **Link** | `url` |

## 🚀 Examples

### Search for Porsche 911 auctions

```
{
  "searches": ["Porsche 911"],
  "maxItems": 100
}
```

### Get data from a specific listing

```
{
  "startUrls": [
    {"url": "https://bringatrailer.com/listing/2007-porsche-boxster-s-24/"}
  ]
}
```

### Browse all BMW E30 M3 results

```
{
  "startUrls": [
    {"url": "https://bringatrailer.com/bmw/e30-m3/"}
  ],
  "maxItems": 50
}
```

### Fast mode without detail pages

```
{
  "searches": ["Ferrari"],
  "maxItems": 200,
  "includeDetails": false
}
```

## 💻 Integrations

### Python

```
from apify_client import ApifyClient

client = ApifyClient("<YOUR_API_TOKEN>")

run = client.actor("silentflow/bringatrailer-scraper").call(run_input={
    "searches": ["Porsche 911"],
    "maxItems": 100,
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item['title']}: {item['priceFormatted']} ({item['totalBids']} bids)")
    print(f"  VIN: {item.get('vin', 'N/A')} | {item.get('mileage', 'N/A')} miles")
```

### JavaScript

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: '<YOUR_API_TOKEN>' });

const run = await client.actor('silentflow/bringatrailer-scraper').call({
    searches: ['Porsche 911'],
    maxItems: 100,
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => {
    console.log(`${item.title}: ${item.priceFormatted} (${item.totalBids} bids)`);
});
```

## 📈 Performance

| Metric | Value |
| --- | --- |
| Search results | ~24 per page from BaT browse |
| Detail enrichment | ~2-3 seconds per listing |
| Fast mode (no details) | Instant for search results |
| Data freshness | Real-time from BaT |

## 💡 Tips for best results

1. **Be specific with keywords.** "BMW E30 M3" returns exactly what you want. "BMW" returns everything.
2. **Browse page URLs for model tracking.** `/porsche/911/` gives you the most recent completed auctions for that model, perfect for price tracking.
3. **Disable detail enrichment for speed.** Set `includeDetails: false` to skip VIN/specs and get just prices and titles. 10x faster for large searches.
4. **Direct listing URLs for full data.** Paste a specific BaT listing URL to get complete specs, all photos, and the full description.

## ❓ FAQ

**Q: Can I get active/ongoing auctions?**
A: Active auctions require a BaT account. This scraper focuses on completed auctions, which are publicly accessible and include final sold prices.

**Q: How far back does the data go?**
A: BaT has auction results going back to their early years. Browse pages show the most recent results first.

**Q: Why are some fields missing (VIN, mileage)?**
A: Not all listings include every field. VIN and mileage depend on what the seller provided. The scraper returns everything available.

**Q: Is the price the final sold price?**
A: Yes. `price` is the hammer price (final bid). For reserve-not-met auctions, `status` will indicate that.

## 📬 Support

Need something this scraper doesn't do yet? We ship features fast.

- 💡 **Feature requests** go straight to our backlog
- ⚙️ **Enterprise needs?** We do custom integrations and high-volume setups

Response time: usually under 24 hours.

Check out our other scrapers: [SilentFlow on Apify](https://apify.com/silentflow)