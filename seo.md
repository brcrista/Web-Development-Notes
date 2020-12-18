# SEO

What is SEO (search engine optimization)?

- Designing site content so that the site can be found through search engines

* My take: PageRank is the fundamental search algorithm.  But there are layers and layers of heuristics that Google has added to point users to high-quality content and penalize ways that people have tried to game the system.

Why is SEO good?

- High return on investment
- Delivers value to users
- Trust and credibility
- Important part of the buying cycle (research)



Four pillars of SEO

1. **Mitigation:** make sure new content is fully optimized
2. **Analysis:** how much did our SEO actions increase our traffic and ranking?
3. **Growth:** what new keywords are trending?
4. **Relationships:** units in an organization need to collaborate



## How search works

- Bot visits a homepage and crawls the links on the homepage
- Content is processed for keywords, which is stored in a cache
- Google scores each page in the cache for relevance to the search and returns the results in order
  - Other things Google looks at: what the site is about ("nature" of the site), language, authority / reliability of the information on a site



### Nature

What kind of site is it?  Some examples of categories:

- Videos
- News
- E-commerce
- Blog
- Social media
- SaaS



### URL structure and SEO

* Google tries to understand the site through the directory structure
* Google now treats subdomains pretty much the same as subdirectories since that is how many sites have come to use them (e.g. vanity URLs)
  * Subdomains still have separate robot.txt
* If a URL doesn't have an extension at the end, it is considered a directory
* At GitHub, we have very deep subdirectories (3-4 deep), which makes things harder for SEO



Other domains we own: github.blog, atom.io.  Google considers these completely separate.

So, it sounds like we actually keep our blog on a separate domain on purpose.  This improves search results for both the blog and content on GitHub proper.



## Keywords

Three things about keywords:

1. Keyword analysis
2. Estimating ROI
3. When not to SEO



Not from this talk, but Instagram PM's advice for optimizing hashtags: choose a small, medium, large, and XL keyword to target.

Keyword plan: keywords + volume

- Take Google's numbers with a grain of salt, since they want you to spend money on advertising

*  `@seogoddess` recommends having each page have its own keyword profile and avoiding duplicating effort (keyword cannibalization, you get penalized by Google for this)
  * Use folders to organize the keyword structure, and then use links to point to the authoritative source for each thing



When estimating ROI, the analysis goes like building a table of our current clickthrough rate on each keyword and the additional percentage points we think we gain

* Current clickthrough rate (CTR)
* A unique page view is when someone clicks on a result
* Unique page views = CTR * volume
* Then you can convert page views to sales and average $ spent for each sale.  That is the ROI.



When not to SEO

* Image-heavy
* Low search volume
* Very technical language (= low search volume)
* User intent doesn't match



## Customer Journey

1. Problem identification
2. Research
3. Engage and connect
4. Evaluate vendors
5. Purchase decision



The **vast** majority of searches are done in 1 and 2.




## Tools

- You can use the [Google Search Console](https://search.google.com/search-console/about) to analyze your site's search performance.
- [Botify](https://www.botify.com/)



## Content

- **EAT**: expertise, authoritativeness, trustworthiness
- Answering questions ("What is DevOps?")
- Google has a patent on **neural matching:** trying to understand user intent behind the search



### Google's principles

* These increase your rank
  * Local content
  * Matching user intent
  * Good UX
  * Accessibility
  * Mobile optimization
* These decrease your rank
  * Plagiarism
  * Spam and keyword stuffing
  * Too many ads or affiliate links
  * Links to unrelated content
  * Broken links



### What bots look for in content

* Keywords
* Unique words
* Title and headings
* Metadata
* Image alt text

### Other stuff that is important for SEO

* GSC owner validation
* robots.txt
* Structured data: XML sitemap, breadcrumbs, FAQs

robots.txt can be used to streamline SEO and tell the bot how to crawl your site to find what's important.

Example: here's GitHub's [robots.txt](https://github.com/robots.txt).

Wordpress will automatically handle the and some structured data.



## Spam

Google tries to provide the best search experience possible.  Therefore, they will penalize you for anything that is trying to game the system or is low-value or negative-value content.

* Generated content
  * Ex. e-commerce product feeds
  * Querying Google keywords and generating feeds based on that
* Link schemes: link to my page and I'll link to your page or pay you
* Plagiarism
  * Pages with little or no original content
  * Scraped content
* Cloaking
  * Putting an image over text
  * Using JavaScript to render text dynamically
  * Text or links hidden with CSS or white-on-white background
* Sneaky redirects
* Malicious pages (e.g. phishing)
* Over-optimizing (`@seogoddess` has seen that you get penalized for too much SEO, "being too perfect")

