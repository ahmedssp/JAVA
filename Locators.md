<img width="1901" height="946" alt="image" src="https://github.com/user-attachments/assets/42846d64-8221-48a1-8749-baf35728b4d2" />
Correct Way (Recommended)
✅ Step 1: Go up to the <tr>
✅ Step 2: Select the correct <td> by position
Final Correct XPath
//tbody//span[text()='https://screenrec.com/share/uXLZRP0FmV']
  /ancestor::tr
  /td[5]


🔹 ancestor::tr → goes to the row
🔹 td[5] → the time column (adjust index if needed)

From your screenshot, the time appears to be the 5th <td>.

If You Want It Relative (Safer)

Instead of hardcoding the URL:

//tbody//tr[.//span[contains(text(),'screenrec.com/share')]]/td[5]


This works even if the URL changes.

Alternative: Based on the URL <td> Position

If the URL is in td[4], then time is the next one:

//tbody//span[text()='https://screenrec.com/share/uXLZRP0FmV']
  /ancestor::td
  /following-sibling::td[1]


✔ This is clean and very stable
