# Penn Dining App

## Description
University of Pennsylvania Dining app that displays the retail and residential dining options on campus, its open and closed times, and presents a link to each venues’ additional info page. 


<img src="https://github.com/angelalin01/diningApp/blob/master/penn%20dining%20page%201.png" alt="alt text" width="500" height="1000"> <img src="https://github.com/angelalin01/diningApp/blob/master/penn%20dining%20page%202.png" alt="alt text" width="500" height="1000">




## Features
- Interfaces and fetches information about Penn's dining options from its backend dining API
- Displays and updates in real time the retail and residential dining options on campus, its open/close times and images of the dining hall. Allows user to scroll through all options.
- Presents a navigation scheme to transition the page to a web view of each venue’s daily menu when user clicks on desired dining hall
- Caches dining hall images using KingFisher image caching library so they are not downloaded each time. 

## Requirements
- iOS 8.0+
- XCode version 10.1
- Swift 4 (Kingfisher 4.x), Swift 3 (Kingfisher 3.x), Kingfisher is a third party library used for image caching

## Installing Kingfisher
`<sudo gem install cocoapods>`

## Running the App
- Download project from https://github.com/angelalin01/diningApp/tree/master/diningAppFINAL and open the workspace in XCode
- Build proejct and run app on the XCode iPhone Simulator 

## Classes and App Design:

- NetworkManager.swift: contains method that makes a network call to the given API and fetches the data for each venue using URL Session. Calls dataToVenues helper method to turn jSON data into a Venue object
- Venue.swift: presents structure of the Venue object (a struct that extends Codable) which emulates the hierarchy of the json data in the API call 
    - Contains a dataToVenues helper function which takes the fetched jSON data as input and uses JSON Decoder to parse the data into a Venue object. Returns an array of Venues 
- UITableViewController: handles most of the app’s logic, populating the TableView with the desired information of each Venue from the API’s data. 
    - Makes asynchronous network call by calling method in NetworkManager. In the closure of the network call, populates several local arrays with the fetched data, while further categorizing venues into “dining” and “retail” options. The final data structure that is used to populate the table cells is a 2D array, [[Venue], [Venue]] where the first element is an array of dining Venues and the second element is an array of retail Venues. This 2D array is used to split up the table view into two sections, one of the dining venues, the other for retail. 
    - Goes through each venue’s daily opening times to see which ones correspond to today’s date and only displays those times, properly formatted per Zeplin specifications. Uses Date() and DateFormatter(). 
    - Populates each tableView Cell with the image, venue name and opening times. Image call is asynchronously done. 
- diningCell.swift:
    - All the display elements that will go into the diningCell, outlets connected from storyboard
    - Contains programmatic constraints for the venue image 
- WebViewController.swft: configures web view and loads the venue's facility website when user clicks on table view cell 


## Improvements and additional features if I had more time: 

- Formatting
    - Playing around more with constraints to ensure label’s texts can be fully displayed in one line without changing the size of the text
- Allowing users to favorite dining halls
