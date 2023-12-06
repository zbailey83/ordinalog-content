# OrdinalOG Content Gen V0.01 Beta

Custom instructions:

Do not use footnotes
Do not link source
Always internally link
Always create tables and lists to break up large walls of text
write one complete comprehensive article
always use product images
Always have logical titles throughout the article with keywords from other articles
Make a comparison table using the product information and images, this table should have all of the information about the products in it


Change keyword at the bottom - send this prompt to ChatGPT Pro

Search for the keyword on Bing, find a page that isn't a category or collection page, and try to understand how it is ranking. Always translate the keyword into the language. Use this to then research the SERP and the results, I will compete with these with an article. Just do the first 5 SERP results. You must search at least 5 websites. Don't overcomplicate things as you keep timing out

Check the SERP for any other useful information, for example people also asked section

Do not output anything just say I'm ready to produce the outline now

In this stage, do all of the research and then say "i'm ready to produce the competitor research now" and wait for user input to create the competitor research

The competitor research should look at several factors:

- How the competitors are ranking
- The unique style of each competitor, and their framing
- Any unique data that the competitors may have
- What we can easily copy and incorporate (without copying exact content)
- NLP keywords and related terms
- Specific expert advice from article
- Word count

From this data, then choose a title and correct framing for this article



Keyword:

Bitcoin Ordinals

Language:

English

—--------------------------------—--------------------------------—--------------------------------


Wait for it to complete the research, then say:

Give me the competitor research table

—--------------------------------—--------------------------------—--------------------------------

Collect your product images, I would recommend using a script similar to the one I showed you in this video, if you’re on shopify you should just be able to input that exact script and just change the URL - You can use this script just change the two URLs

Ask it now to create a comparison table using as much information as possible from your product image list 

Create a comparison table for these products, try to include as much information and as many products as possible, add product images inside the table and make them clickable

—--------------------------------—--------------------------------—--------------------------------

Using both the product comparison table and the competitor research table, now create an outline for an article for my website

Using both the product comparison table for information, and the competitor research table for ideas and things to write about, now create an outline for an article

—--------------------------------—--------------------------------—--------------------------------







Use the final prompt below, change it to fit your business

Do not use footnotes 

Output content in Markdown. Only use an internal link once. Use your best writing ability to create an essay for my website, OrdinalOG.com. The go-to-website and source for  the latest and most knowledgable news, guides & infromation on the following subjects, within the Cryptocurrency ecosystem, “Bitcoin”, “Ordinals”, “NFT”s, “Inscriptions”, “BRC-20 Tokens” and more. 


Use burstiness and creativity when writing.

Write in professional English. Try to use simple, basic English that is completely correct and conversational.

Iternal links add https:/ordinalog.com/ before each:

/section/bitcoin-trading
/section/bitcoin-nfts
/section/ordinals
/section/bitcoin-ordinals
/section/inscriptions
/section/bitcoin-inscriptions
/section/brc-20s
/section/trending-topics
/section/nfts

Use these products to create an essay about the translated keywords from before Before you start look at this page to understand. Please create a table summarizing all of the information at the top of the essay, in a key takeaways table. This table should answer any questions someone might have when coming to this page. Also use lists, and other HTML formatting in order to make the page more readable.





import requests
from bs4 import BeautifulSoup
import json
import re


def get_html(url):
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.text
    except requests.RequestException as e:
        print(f"Error fetching {url}: {e}")
        return None


def extract_json_data(script_content):
    try:
        json_data_match = re.search(r'webPixelsManagerAPI.publish\("collection_viewed", (\{.*?\})\);', script_content)
        if json_data_match:
            json_data = json.loads(json_data_match.group(1))
            return json_data
        else:
            print("JSON data match not found in script content")
            return None
    except json.JSONDecodeError as e:
        print(f"Error decoding JSON: {e}")
        return None


def extract_product_info(json_data):
    product_info = []
    for variant in json_data["collection"]["productVariants"]:
        product_url = f"https://domain.com{variant['product']['url']}"
        image_url = f"https:{variant['image']['src']}"
        price = variant['price']['amount']
        product_info.append({
            "title": variant['product']['title'],
            "url": product_url,
            "image_url": image_url,
            "price": f"€{price:.2f}"
        })
    return product_info


# URL of the category page
category_url = "https://domain.com/kiton"


# Fetch the HTML content of the category page
category_page_html = get_html(category_url)
if category_page_html:
    soup = BeautifulSoup(category_page_html, 'html.parser')
    script_tag = soup.find('script', {'id': 'web-pixels-manager-setup'})
    if script_tag:
        json_data = extract_json_data(script_tag.string)
        if json_data:
            product_info = extract_product_info(json_data)
            for info in product_info:
                print(info)
        else:
            print("Failed to extract JSON data from script")
    else:
        print("Script tag with the specified ID not found")
else:
    print("Failed to fetch category page HTML")



