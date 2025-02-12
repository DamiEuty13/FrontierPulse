pip install streamlit pandas yfinance requests
import streamlit as st
import pandas as pd
import requests

# Alpha Vantage API for South Africa's stock index (JSE)
def get_jse_data():
    API_KEY = "YOUR_ALPHA_VANTAGE_KEY"
    url = f"https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=JSE.JO&apikey={API_KEY}"
    response = requests.get(url).json()
    data = pd.DataFrame(response["Time Series (Daily)"]).T
    return data

# Display data in Streamlit
st.title("Africa Markets")
st.write("South Africa JSE All Share Index")
st.line_chart(get_jse_data()["4. close"])

st.markdown("""
<div class="tradingview-widget-container">
  <script type="text/javascript" src="https://s3.tradingview.com/external-embedding/embed-widget-forex-cross-rates.js">
  {
    "currencies": ["EUR", "USD", "NGN", "ZAR", "EGP", "KES"],
    "isTransparent": false,
    "colorTheme": "light",
    "locale": "en"
  }
  </script>
</div>
""", unsafe_allow_html=True)

africa_tab, asia_tab, middle_east_tab, latam_tab = st.tabs(["Africa", "Asia", "Middle East", "Latam"])
with africa_tab:
    # Display Africa data

def get_news(region):
    API_KEY = "YOUR_NEWSAPI_KEY"
    url = f"https://newsapi.org/v2/everything?q={region}+economy&apiKey={API_KEY}"
    articles = requests.get(url).json()["articles"]
    return articles

st.header("Latest News")
for article in get_news("nigeria"):
    st.write(f"**{article['title']}**")
    st.write(article["description"])

from pandas_datareader import wb

# Fetch GDP for Nigeria
gdp_data = wb.download(indicator="NY.GDP.MKTP.CD", country=["NG"], start=2020, end=2023)
st.line_chart(gdp_data)
