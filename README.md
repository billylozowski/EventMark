# EventMark
This code uses time series data to automatically mark key timepoints of a biomechanical motion.

Chunk:
1. Imports the file of interest (currently a .txt file) and removes redundant rows
   Creates two new columns called "Events" and "Time (s)"
   
2. Calculates front-foot contact from force plate data
  - The current threshold is the first frame where force data exceeds 20N, but adjust this as needed
  
3. Calculates front-foot contact from position data (if force data is not available)
  - This chunk is current set up to be skipped {r eval = FALSE}
  
4. Calculates back-foot contact from AP ankle velocity and vertical ankle acceleration
  - The setup we use is a vertical axis of _Y_, an AP axis of _X_, and a ML axis of _Z_
  
5. Calculates maximal arm withdrawal
  - The most posterior position (AP) of the upper-arm's centre of mass relative to the thorax
  
6. Calculates ball release from the hand linear velocity
  - The maximum value +2 frames
  
7. Calculates the end of the follow-through from hand AP position
  - The most posterior position of the hand in the AP direct after ball release
    > This is the point where the arm is wrapped across the chest, and begins to recoil
    
8. Mark the index of each event as a 1 in the data frame "data"

9. Calculate the percentage of each frame with respect to throw duration (BFC to EFT)
  - BFC = 0%
  - EFT = 100%

10. Saves the event-marked trial as a .csv file wherever the user desires

11. Using the event indices, extract all columns at each of the specified event rows

12. Find the minimum and maximum values for each column and bind to the bottom of the extracted event data

13. SAve the event data, plus the minimum and maximum values as a .csv file wherever the user desires
    