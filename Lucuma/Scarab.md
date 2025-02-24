# Scarab Pest Monitoring Software
## Architecture

- **Post-Login Interface**
  - Top Bar and Side Navigation (Sidenav)
  - Dashboard displays cards for each farm
  - Sidenav options:
    - **Farm** (current location)
    - **Trends by Farm**
    - **Reports**

- **Farm-Specific Navigation**
  - When a farm is selected, the sidenav changes to:
    - **Precision**
    - **Action**
    - **Farm Settings**

- **Detailed Farm Modules**

  **Farms Module**
    - **Select Farm**
      - **Precision**
        - **Scouting**
          - *Stacked Gantt Chart*: Displays blocks covered per worker over the schedule.
          - *Table 1*: Summarizes:
            - Total number of beds (sum)
            - Average stations per bed
            - Minutes per bed
          - *Table 2*: Lists:
            - Incomplete sectors
            - Sector variability
            - Recorded bed number
            - Required number of beds
          - *Map*: Shows the path and locations visited by the worker.
        - **Maps**
          - *Heatmap Table*: 
            - Columns: Station (with rose variety indication)
            - Rows: Beds per block per pathogen
            - Time Range: Adjustable filter over a range of dates
        - **Panorama**
          - *Map with Heatmap Overlay*: Provides a farm-wide view similar to the heatmap.
        - **Tables**
          - *Data Table*: Includes date, block, sector, pathogen attributes, and worker information.
        - **Trends**
          - *Line Chart*: Displays pathogen area over time with each sector of a block represented by a different line.
        - **Partitions**
          - *Note*: Data structure and usage are not yet defined.
        - **Traps**
          - *Map*: Displays trap locations per block over time (interior, exterior, post-harvest) and monitors pathogen trips.

      - **Action**
        - **Action Results**
          - *Timeline*: Displays results per block per pathogen and shows the kit used (a kit is a combination of products in varying amounts).
          - *Playground*: An interactive workspace for testing and visualizing actions (details to be defined).
          - *Done*: Calendar view showing completed tasks and events.
        - **Action Plan**
          - **Spray**
            - *Module Description*: Manages pesticide application scheduling.
            - *Details Included*: Pesticide mix/kit used, application timing, dosage per block and bed, and spray type.
        - **Stocktaking**
          - **Budget (Monthly)**
            - *Summary Table*: Shows monthly budget, total spent, and current balance.
            - *Detailed Expenses Table*: Breaks down individual expense items.
          - **Loan**
            - *Action Button*: Option to request a chemical loan.
          - **Reconciliation**
            - *Table*: Lists product, planned amount, actual amount, units, and the difference; includes user identifiers.
        - **Rotation**
          - **Tank Mixes**
            - *Table*: Contains:
              - Products
              - Mechanism of Action (MoA)
              - Application rate per product (e.g., cc/l, g/l)
              - Volume per bed
              - pH, hardness, pressure, and strata information
          - **Products**
            - *Table*: Lists product formulations, intended uses, active ingredients, and concentrations.
          - **Blacklist**
            - *Table*: Contains products that are disallowed.
        - **Kits**
          - **Spray Kits**
            - *Cards*: Each kit is presented as a card.
            - *Card Details*: Includes a table with kit components and a description.
          - **Operators**
            - *Table*: Lists operator names and positions (roles).
          - **Rules**
            - *Thresholds*: Likely used to set application limits (exact purpose to be defined).
            - *Sensitivity*: Likely used for adjusting alert or application thresholds (exact purpose to be defined).

      - **Farm Settings**
        - **Foliage**
          - *Purpose*: Likely describes crop varieties and states (e.g., productive beds).
          - *Table*: Lists block, sector variability, and foliage details.
        - **Beds**
          - *Summary Table*: Provides the farm-based median bed count (single number) and house-based median beds, with results in meters (or distance units).
          - *Distribution Table*: Shows bed lengths on the farm (bed length in meters) and their frequency.
        - **Units**
          - **Hose Length**
            - Toggle options: Meter, Foot
          - **Hose Thickness**
            - Toggle options: Millimeter, Inch
          - **Output per Lance**
            - Toggle options: Liter per minute, Cubic meter per minute
          - **Pump Pressure**
            - Toggle options: Pascal, Kilopascal, Bar, Pound per square inch
          - **Tank Volume**
            - Toggle: Specify unit as needed
          - **Volume per Length of Bed**
            - Toggle options: Liter per meter, Milliliter per meter, Liter per bed
          - **Water Hardness**
            - Toggle options: Gram per liter, Parts per million, Milligram per liter

 **Trends by Farms**
  - *Line Chart*: Shows pathogen area over time at specific locations.

 **Reports**
  - *Table 1*: Active ingredients used (quantity per hectare) at a location over a specified time range.
  - *Table 2*: Water volume used at a location over a specified time range.
  - *Table 3*: Toxicological product usage (quantity per hectare) at a location over a specified time range, including product toxicity information.
