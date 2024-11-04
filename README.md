# Synthetic Social Media Data Generator
## Table of Contents
1. [Introduction](#introduction)
2. [Features](#features)
3. [Installation](#installation)
4. [Usage](#usage)
    * [Running the Script](#running-the-script)
    * [Input Prompt](#input-prompt)
5. [Generated Data](#generated-data)
    * [Data Files](#data-files)
6. [Network Analysis](#network-analysis)
    * [Community Detection](#community-detection)
    * [Top Influencers](#top-influencers)
    * [Visualization](#introduction)
7. [Data Validation](#introduction)
8. [Customization](#introduction)
    * [Parameters](#introduction)
    * [Further Enhancements](#introduction)
9. [Dependencies](#introduction)
10. [License](#introduction)
11. [Acknowledgements](#introduction)

## Introduction
The Synthetic Social Media Data Generator is a Python-based tool designed to create realistic synthetic data simulating user interactions and engagement on a social media platform. This tool is ideal for data scientists, analysts, and developers who require large-scale, privacy-compliant datasets for testing, modeling, and analysis without using real user data.

By incorporating user demographics, follower relationships, activity patterns, engagement metrics, influence scores, and network community structures, this generator provides a comprehensive dataset that mimics the complexities of real-world social media platforms.

## Features
- **User Profiles:** Generate user demographic information including age, location, and interests.
- **User Relationships:** Simulate follower-followed relationships influenced by shared interests.
- **Content Metadata:** Define various content types, hashtags, and media attachments.
- **User Activities:** Simulate user activities such as posts, likes, comments, and shares, with dynamic patterns based on time slots (weekday, evening, weekend).
- **Engagement Metrics:** Calculate engagement scores based on user activities.
- **Influence Metrics:** Assess user influence using follower count, engagement, and network centrality measures (PageRank, Betweenness Centrality).
- **Network Analysis:** Detect communities within the user network and identify top influencers.
- **Data Validation:** Ensure data integrity and consistency across all generated datasets.
- **Data Visualization (Optional):** Visualize the community structure of the user network.
- **Customization:** Easily adjust parameters such as the number of users, average followers, and simulation time frame.

## Installation
To set up the Synthetic Social Media Data Generator on your local machine, follow these steps:
1. Clone the Repository:

    ```
    git clone https://github.com/yourusername/synthetic-social-media-data-generator.git
    cd synthetic-social-media-data-generator
    ```

3. Create a Virtual Environment (Optional but Recommended):

    ```
    python3 -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

4. Install Required Dependencies:

    ```
    pip install pandas numpy faker networkx python-louvain matplotlib
    ```

## Usage
### Running the Script
1. **Navigate to the Project Directory:**

    Ensure you are in the directory containing the `generate_synthetic_data.py` script.

2.  **Execute the Script:**

    ```
    python generate_synthetic_data.py
    ```
### Input Prompt
Upon execution, the script will prompt you to enter the directory path where you want to save the generated CSV and analysis files.

```
Enter the directory path to save the CSV files: ./synthetic_data
```
* **If the Directory Exists:** The script will save the files in the specified directory.
* **If the Directory Does Not Exist:** The script will attempt to create it. Ensure you have the necessary permissions.

## Generated Data
The script generates several CSV files containing different aspects of the synthetic social media data. Below is an overview of each file:
### Data Files
1. `user_profiles.csv`
    * **Description:** Contains user demographic information.
    * **Columns:**
      * `user_id`: Unique identifier for each user.
      * `age`: Age of the user.
      * `location`: Geographical location of the user.
      * `interests`: List of user interests.
    
2. `user_relationships.csv`
    * **Description:** Details of follower-followed relationships.
    * **Columns:**
      * `follower_id`: User ID of the follower.
      * `followed_id`: User ID of the user being followed.
    
3. `posts.csv`
    * **Description:** Information about each post made by users.
    * **Columns:**
      * `post_id`: Unique identifier for each post.
      * `user_id`: User ID of the poster.
      * `timestamp`: Date and time when the post was made.
      * `content_type`: Type of content (text, image, video).
      * `hashtags`: List of hashtags associated with the post.
      * `media_attachment`: Media file attached to the post (if any).
      * `quality_score`: Quality rating of the post (1-5).
  
4. `user_activities.csv`
    * **Description:** Logs of all user activities, including posts and interactions.
    * **Columns:**
      * `user_id`: User ID performing the activity.
      * `activity_type`: Type of activity (post, like, comment, share).
      * `timestamp`: Date and time of the activity.
      * `content_type`: Type of content involved in the activity (if applicable).
      * `hashtags`: List of hashtags involved in the activity (if applicable).
      * `media_attachment`: Media file involved in the activity (if applicable).
      * `post_id`: Reference to the associated post (if applicable).
    
5. `engagement_metrics.csv`
    * **Description:** Aggregated engagement scores for each user based on their activities.
    * **Columns:**
      * `user_id`: User ID.
      * `total_posts`: Total number of posts made.
      * `total_likes`: Total number of likes given.
      * `total_comments`: Total number of comments made.
      * `total_shares`: Total number of shares made.
      * `engagement_score`: Calculated engagement score.
    
6. `influence_metrics.csv`
    * **Description:** Influence metrics for each user, assessing their impact within the network.
    * **Columns:**
      * `followed_id`: User ID being followed.
      * `num_followers`: Number of followers the user has.
      * `user_id`: Redundant from merge (can be ignored or removed).
      * `total_posts`: Total number of posts made.
      * `total_likes`: Total number of likes given.
      * `total_comments`: Total number of comments made.
      * `total_shares`: Total number of shares made.
      * `engagement_score`: Engagement score.
      * `influence_score`: Calculated influence score.
      * `pagerank`: PageRank centrality score.
      * `betweenness_centrality`: Betweenness centrality score.
      * `location`: User location.
      * `age`: User age.
      * `interests`: User interests.
      * `community_id`: Community assignment.
    
7. `communities.csv`
    * **Description:** Community assignments for each user within the network.
    * **Columns:**
      * `user_id`: User ID.
      * `community_id`: Identifier for the community the user belongs to.
    
8. `top_influencers.txt`
    * **Description:** Lists the top 10 influencers based on PageRank scores.
    * **Content:** Each line contains a user ID of a top influencer.

## Network Analysis
### Community Detection
The script utilizes the Louvain method for community detection within the user network. This identifies clusters of users who are more densely connected to each other, reflecting real-world communities or interest groups.
* **Output:** `communities.csv` containing `user_id` and their assigned `community_id`.
### Top Influencers
Top influencers are identified based on their PageRank scores, which measure the importance of a user within the network.
* **Output:** `top_influencers.txt` listing the top 10 user IDs with the highest PageRank scores.
Visualization
The script includes an optional feature to visualize the community structure of the user network.
* **How to Enable:**
  1. **Uncomment the Visualization Code Block:**
      ```
      """
      print("Visualizing community structure...")
      plt.figure(figsize=(10, 10))
      pos = nx.spring_layout(G, seed=42)
      cmap = plt.get_cmap('viridis')
      nx.draw_networkx_nodes(G, pos, node_size=50,
                             node_color=communities['community_id'],
                             cmap=cmap, alpha=0.7)
      nx.draw_networkx_edges(G, pos, alpha=0.5)
      plt.title('User Network Community Structure')
      plt.axis('off')
      plt.savefig(os.path.join(output_dir, 'community_structure.png'))
      plt.close()
      """
      ```
  2. **Modify the Code (if needed):** Enhance the color mapping or layout as desired.
  3. **Run the Script:** Upon execution, community_structure.png will be saved in the output directory.

* **Note:** For large networks, visualizing all nodes and edges may result in cluttered images. Consider sampling or focusing on specific communities for clarity.
