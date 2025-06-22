# 🔗 URL Summarizer

This Python script extracts and summarizes textual content from **any webpage URL** using `newspaper3k`, `sumy`, and `nltk`. It uses **Latent Semantic Analysis (LSA)** to generate a concise summary of the content.

---

## 📜 Full Python Code

```python
import nltk
from newspaper import Article
from sumy.parsers.plaintext import PlaintextParser
from sumy.nlp.tokenizers import Tokenizer
from sumy.summarizers.lsa import LsaSummarizer

def get_article_text(url):
    article = Article(url)
    article.download()
    article.parse()
    return article.text

def summarize_text(text, num_sentences=3):
    parser = PlaintextParser.from_string(text, Tokenizer("english"))
    summarizer = LsaSummarizer()
    summary = summarizer(parser.document, num_sentences)
    return ' '.join(str(sentence) for sentence in summary)

def main():
    # Input URL
    url = input("Enter the URL of the website: ")

    # Get article text from the URL
    article_text = get_article_text(url)

    # Summarize the text
    summary = summarize_text(article_text)

    # Display the summary
    print("\nSummary:")
    print(summary)
    print("FOR FURTHER DETAILS PLEASE VISIT THE WEBSITE!!")
    print("THANK YOU :)")

if __name__ == "__main__":
    main()
```

---

## ⚙️ Requirements

Install the required libraries before running the script:

```bash
pip install newspaper3k sumy nltk
```

Also, download the NLTK Punkt tokenizer:

```python
import nltk
nltk.download('punkt')
```

---

## 🚀 How to Run

1. Save the script in a file named `url_summarizer.py`.
2. Open a terminal and run:

```bash
python url_summarizer.py
```

3. Enter a URL when prompted (preferably one containing text like a blog or article).

---

## 🔍 Example

**Sample Input:**

```
Enter the URL of the website:
https://timesofindia.indiatimes.com/world/china/china-tightens-grip-over-internet-during-key-political-meeting/articleshow/108362819.cms
```

**Sample Output:**

```
Summary:
China is increasing internet censorship during a key political meeting.
Access to platforms like Twitter and Instagram is being restricted further.
Authorities are using advanced surveillance tools to monitor online activity.

FOR FURTHER DETAILS PLEASE VISIT THE WEBSITE!!
THANK YOU :)
```

---

## 📌 Notes

- The number of summary sentences can be adjusted in the `summarize_text` function (`num_sentences=3`).
- Works best on text-rich URLs (articles, blogs, etc.).
- Some websites may block scrapers or serve JavaScript-heavy pages, which may not extract properly.

---

## 📁 Project Structure

```
url_summarizer.py   # Main script
README.md           # Documentation
```

---

## 📄 License

This project is free to use and modify for educational and personal use.
