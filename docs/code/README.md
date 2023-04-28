---
tags:
  - INDEX
---

# Docker

Hell yeah dog. NGL.

[Here](https://hub.docker.com/) is the docker hub website! Get learnt.

## Random Notes

links to Home depot stuff I need.

[Garage Door Seal](https://www.homedepot.com/p/M-D-Building-Products-0-25-in-x-2-75-in-x-9-ft-V1046-White-Dual-Vinyl-Garage-Door-Seal-Top-and-Sides-Weatherstrip-87700/205021160)

[T Square](https://www.homedepot.com/p/Empire-48-in-Drywall-T-Square-410-48/202035306)

## Polyiso pieces cut list

### Per panel, I need the following

- Two pieces that are 52.5 inches by 22 inches
- Two pieces that are 1.5 inches by 22 inches
- Two pieces that are 1.5 inches by 52.5 inches

### To calculate the total number of pieces of polyiso foam you'll need, multiply the number of pieces needed for each panel by the total number of panels on both garage doors

- Two pieces that are 52.5 inches by 22 inches per panel x 8 panels per door x 2 doors = 32 pieces
- Two pieces that are 1.5 inches by 22 inches per panel x 8 panels per door x 2 doors = 32 pieces
- Two pieces that are 1.5 inches by 52.5 inches per panel x 8 panels per door x 2 doors = 32 pieces

Therefore, you'll need a total of 96 pieces of polyiso foam for both garage doors.

## garage door outdoor measurements

For the exterior trim/moulding, the following measurements.

W 106.5
H 83

## Garage door indoor/panel measurements

W 52.5
H 21 ish?

## garage door bottom/actual width

W 108.5

## misc

Panels:

8 per door at 52.5x21

## game room door/windows

W 46-46.5
H 80-80.5

### glass for right window

H 73.5
W 43.75

## Calculate the total amount of shit I need

Sure, I can help you figure out how many sheets of polyiso foam you'll need for your project. Here are the steps:

1. Calculate the total area of each garage door panel. Each panel is 52.5 inches wide and 22 inches tall, so the total area of each panel is:

    ```ruby title="Total Area: Garage Panel"
    52.5 inches x 22 inches = 1155 square inches
    ```

2. Convert the area of each panel to square feet. There are 144 square inches in a square foot, so the area of each panel in square feet is:

    ```ruby title="SQ ft per Panel"
    1155 square inches / 144 = 8.03 square feet
    ```

3. Calculate the total area of all the panels on both garage doors. Each garage door has 8 panels, so the total area of all the panels on both doors is:

    ```ruby title="Total Area: All Panels"
    8 panels x 2 doors x 8.03 square feet per panel = 128.48 square feet
    ```

4. Calculate the number of polyiso foam sheets you'll need. Each polyiso foam sheet is 4 feet wide and 8 feet tall, which is 32 square feet. Divide the total area of all the garage door panels by the area of each polyiso foam sheet to get the number of sheets needed:

    ```ruby title="Total Sheets Needed"
    128.48 square feet / 32 square feet per sheet = 4.015 sheets
    ```

5. Round up to the nearest whole sheet to account for any waste or errors

Hence, 5 pieces of foam.

## Cut list to make the most efficient use of the polyiso foam sheets

1. For the two pieces that are 52.5 inches by 22 inches, cut each sheet of polyiso foam into four pieces that are 2 feet by 4 feet. Then, cut each of these 2 feet by 4 feet pieces into two pieces that are 52.5 inches by 22 inches. This will give you a total of 16 pieces that are 52.5 inches by 22 inches.

2. For the two pieces that are 1.5 inches by 22 inches, cut each sheet of polyiso foam into strips that are 1.5 inches wide and 8 feet long. Then, cut each strip into pieces that are 22 inches long. You'll get 64 pieces that are 1.5 inches by 22 inches.

3. For the two pieces that are 1.5 inches by 52.5 inches, cut each sheet of polyiso foam into strips that are 1.5 inches wide and 4 feet long. Then, cut each strip into pieces that are 52.5 inches long. You'll get 32 pieces that are 1.5 inches by 52.5 inches.

So, to shorten that up, here is a truncated cut list:

```cs title="Cut List"
pieces:
  52.5 inches by 22 inches
    32 pieces
  1.5 inches by 22 inches
    32 pieces
  1.5 inches by 52.5 inches
    32 pieces
```
