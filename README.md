# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
    import pandas as pd
    data=pd.read_csv("SAMPLEIDS.csv")
    df=pd.DataFrame(data)
    df

<img width="1358" height="473" alt="image" src="https://github.com/user-attachments/assets/7621428f-abfe-420c-aa3b-8f164e66815b" />

    df.info()

<img width="661" height="357" alt="image" src="https://github.com/user-attachments/assets/236343a8-b702-4c79-a5e8-79cf8ac43f07" />

    df.describe()

<img width="953" height="323" alt="image" src="https://github.com/user-attachments/assets/0b607ff4-aef2-4f4e-a70e-176e70b38c38" />

    df.isna().sum()

<img width="525" height="231" alt="Screenshot (75)(1)" src="https://github.com/user-attachments/assets/f183feab-8723-48fe-bd36-bdf0839168d0" />

    df.fillna(0)

<img width="1021" height="693" alt="image" src="https://github.com/user-attachments/assets/83eba9cb-19b0-4ce7-bd58-73e2456053db" />

    df.fillna(method="ffill")

<img width="1083" height="697" alt="image" src="https://github.com/user-attachments/assets/37a84f81-26bf-452c-9e6f-9c6e7c4c898a" />

    f.fillna(method="bfill")

<img width="1056" height="689" alt="image" src="https://github.com/user-attachments/assets/88790f9f-c895-4fce-8a00-9a818288be00" />

    df["TOTAL"].fillna(df["TOTAL"].mean())

<img width="1064" height="686" alt="image" src="https://github.com/user-attachments/assets/fb4d6091-29bb-4882-a21f-7851e04626bc" />

    df.dropna(axis=0,inplace=True)

<img width="1328" height="613" alt="image" src="https://github.com/user-attachments/assets/af62fa3a-00f6-4676-878c-451816ac7ad3" />

    df.to_csv('newdata1.csv', index=False)
    data1=pd.read_csv("newdata1.csv")
    df=pd.DataFrame(data1)
    df

<img width="1348" height="608" alt="image" src="https://github.com/user-attachments/assets/88fd06c3-895b-4f69-a189-905f6922b372" />

    df["num_episodes"]

<img width="552" height="263" alt="image" src="https://github.com/user-attachments/assets/02c0075e-c677-4d1a-af97-4fc151a4cbf9" />

    import seaborn as sns
    import numpy as np
    sns.boxplot(data=df["num_episodes"]) #before removing outliers

<img width="1005" height="543" alt="image" src="https://github.com/user-attachments/assets/c98a49fa-d88c-49db-a3c3-cfbc94f2ee0e" />

    sns.scatterplot(data=df["num_episodes"]) #before removing outliers

<img width="858" height="582" alt="image" src="https://github.com/user-attachments/assets/d0324405-06db-4c07-953c-d1a1ee7c6a5a" />


    #USING IQR METHOD ON THE COLUMN "NUM_EPISODES"

    q1=df["num_episodes"].quantile(0.25)
    q3=df["num_episodes"].quantile(0.75)
    IQR=q3-q1
    up_bound=q3+(1.5*IQR)
    low_bound=q1-(1.5*IQR)
    outliers=[x for x in df["num_episodes"] if x<low_bound or x>up_bound]
    print("q1:",q1)
    print("q3:",q3)
    print("IQR:",IQR)
    print("upper bound:",up_bound," and lower bound:",low_bound)
    print("Outliers:",outliers)

<img width="612" height="122" alt="image" src="https://github.com/user-attachments/assets/183f42a3-c750-465e-a7d6-e36055da6618" />

    #USING Z-SCORE METHOD ON THE COLUMN "NUM_EPISODES"

    mean=np.mean(df["num_episodes"])
    std=np.std(df["num_episodes"])
    threshold=3
    outliers=[]
    for i in df["num_episodes"]:
        z=(i-mean)/std
        if np.abs(z)>threshold:
            outliers.append(i)
    print("Mean:",mean)
    print("Standard deviation:",std)
    print("Outliers:",outliers)


<img width="1018" height="83" alt="image" src="https://github.com/user-attachments/assets/94fcaced-dcc0-4db5-9d26-2175825dd4ce" />

    #droping outliers(num_episodes=50)
    index_to_delete = df[df["num_episodes"] == 50].index
    df.drop(index_to_delete, inplace=True)

<img width="1337" height="624" alt="image" src="https://github.com/user-attachments/assets/cbf8109a-1878-48f6-aa6d-4ab4a2534be4" />

    sns.scatterplot(data=df["num_episodes"]) #after removing outliers

<img width="1341" height="552" alt="image" src="https://github.com/user-attachments/assets/5a91bbb6-6bbe-4952-b2e5-52bc5f410a83" />

    sns.boxplot(data=df["num_episodes"]) #after removing outliers

<img width="1380" height="540" alt="image" src="https://github.com/user-attachments/assets/806ef627-9bba-403b-a707-2ff4e00e0ded" />    
            
            
            
                

# Result
 Thus the program to read the given data and perform data cleaning and save the cleaned data to a file and removing outliers using IQR method and Z-score method is written and executed successfully.
