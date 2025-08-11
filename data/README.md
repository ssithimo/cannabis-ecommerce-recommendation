# Assumptions for Simulated Cannabis E-Commerce Dataset (100 rows)

---

## 1. Product Attributes
   
  - Product ID: Unique identifier (e.g., "p001", "p002", ...)

  - Product Name:

    - Varies by strain + format + quantity (e.g., "OG Kush 1/8 oz", "Blue Dream Vape Cartridge 500mg")

    - Includes common cannabis strain names (OG Kush, Blue Dream, Girl Scout Cookies, etc.)

    - Product types: flower, vape, edible, concentrate

    - Naming inconsistencies (e.g., "OG Kush 1/8 oz" vs. "OG Kush Eighth", or typos)

  - Category: One of {“Hybrid Flower”, “Sativa Flower”, “Indica Flower”, “Vape Cartridge”, “Edible”, “Concentrate”}

  - Vendor Name: Simulate ~10 different vendors with realistic names

  - THC %: Range from ~15% to 30% for flowers, or potency in mg for vapes/edibles (e.g., 500mg THC)

  - CBD %: Range from 0% to 5% typically

  - Price: Based on product type and quantity, e.g., $20-$60 for 1/8 oz flower, $30-$60 for vape cartridges

  - Availability: Boolean or inventory count (e.g., 0-100 units)

  - Description: Short text with strain effects, flavor notes, or product benefits (semi-randomized)

  - Tags: List of keywords (e.g., “relaxing”, “uplifting”, “citrus”, “pain relief”)

  - Date Added: Recent date within last 6 months

## 2. Data Inconsistencies / Noise

  - Include misspellings or alternate product names

  - Random missing values for THC% or CBD% (to simulate real messy data)

  - Some products have incomplete descriptions

  - Vendor names may vary slightly (e.g., “GreenLeaf Co.” vs “Green Leaf Co.”)

  - Categories sometimes mislabeled or abbreviated (“Sativa”, “Indica”, “Hybrid”, “Vape”, etc.)

## 3. Relational Structure

  - Products linked to vendors and categories

  - Multiple products from same vendor with slight variations

  - Some duplicate or near-duplicate products (to test similarity matching)

## 4. User Behavior (might create a new dataset for rdbms with product id as key)

  - Could simulate user search queries or purchases later, but not in initial 100 rows
