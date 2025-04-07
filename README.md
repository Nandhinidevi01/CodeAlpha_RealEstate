import pandas as pd

# Load your CSV dataset
df = pd.read_csv("C:/path/to/real_estate_data.csv")

# Ensure date parsing
df['DateListed'] = pd.to_datetime(df['DateListed'], errors='coerce')

# Calculate Rental Yield (%)
df['RentalYield'] = (df['Rent'] * 12) / df['Price'] * 100

# Clean data
df = df.dropna(subset=['City', 'Price', 'Rent', 'Latitude', 'Longitude'])

# Create buckets for price heatmap
df['PriceBucket'] = pd.cut(df['Price'], bins=[0, 200000, 400000, 600000, 800000, 1e6, 1.5e6, 2e6], 
                           labels=["<200k", "200k-400k", "400k-600k", "600k-800k", "800k-1M", "1M-1.5M", ">1.5M"])

# Output to Power BI
df
