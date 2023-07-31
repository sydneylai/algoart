objects: https://craftpix.net/freebies/free-staves-2d-weapon-pack/ <br>
characters: https://craftpix.net/freebies/2d-fantasy-elf-free-sprite-sheets/ <br>
background: https://craftpix.net/freebies/free-elven-land-game-battle-backgrounds/

# Create and host NFTs with 25 lines of code

You often hear about the 10,000 NFT collection, but how does someone make thousands of unique images? Today we will build an algorithmically generate image dataset and host them on IPFS as a unique NFT. 

We host the images in [IPFS](https://ipfs.io/) because this a peer to peer and a decentralized form of storage, rather than a centralized solution like AWS or Google Cloud. Therefore if AWS goes down or you forget to pay your Cloud subscription, you still have a hosting solution that assigned a unique identifier or content identifier (CID).

Once you have a unique image, you can either distribute your NFTs on a marketplace, put it on a smart contract or turn it into a game. I'll include resources below for how else you can continue to build. This tutorial is for absolute beginners who want to learn how to create and host their NFTs.  

**Tools you'll need:**

- Python
- [Pillow Library](https://pillow.readthedocs.io/en/stable/)
- [NFT Storage](https://nft.storage/)

**Download Images**


[Consolidated Folder](https://github.com/sydneylai/generateNFT) found on my Github



Otherwise, if you want to create your own selection:

- objects: https://craftpix.net/freebies/free-staves-2d-weapon-pack/
- characters: https://craftpix.net/freebies/2d-fantasy-elf-free-sprite-sheets/
- background: https://craftpix.net/freebies/free-elven-land-game-battle-backgrounds/

## Create Image Folders 

Create a master folder, you can name it "NFT1"
Create a folder to organize your:

1. backgrounds
2. characters
3. objects

## Code Breakdown

Install Pillow Library
```
pip install Pillow
```
Go into python, create a python file name "<span>main.py</span>"

```
emacs main.py
```
In your python file, you want to include the following code. 

Here is the python code needed to create your image collection.
```python

from os import path, mkdir
from PIL import Image

output_folder = "generated"
if not path.exists(output_folder):
    mkdir(output_folder)

def generate_image(background, character, object, file_name):
  background_file = path.join("backgrounds", f"{background}.png")
  background_image = Image.open(background_file)

  #Create character
  character_file = path.join("characters", f"{character}.png")
  character_image = Image.open(character_file)
  coordinates = (int(1920/2-character_image.width/2), int(1000-character_image.height)) #x, y
  background_image.paste(character_image, coordinates, mask=character_image)

  #Create object
  if object != "none":
    object_file = path.join("objects", f"{object}.png")
    object_image = Image.open(object_file)
    coordinates = (int(1920/2+character_image.width/2+30), int(1000-object_image.height)) #x, y
    background_image.paste(object_image, coordinates, mask=object_image)
    output_file = path.join(output_folder, f"{file_name}.png")
    background_image.save(output_file)

for background in ["background1", "background2", "background3"]:
    for character in ["elf1", "elf2", "elf3"]:
        for object in ["object1", "object2", "object3"]:
            generate_image(background, character, object, file_name=f"{background}{character}{object}")
            
   
```

## Coordinates

Calculating the coordinates is how you will layer the image files on top of each other. For example, if you have collectable dogs and they have objects like hats, you will be able to place various hats on the template frame of the dog image.


Calculate the length and width of your background image, and know where to place your characters. 


```python
coordinates = (int(1920/2-character_image.width/2), int(1000-character_image.height)) #x, y
```


Calculate the length and width of your background image, and know where to place your objects. 
```python
coordinates = (int(1920/2+character_image.width/2+30), int(1000-object_image.height)) #x, y
```
Special thanks to Albert Sanchez Lafuente. If additional math is needed for figuring out coordinates on your image [read](https://towardsdatascience.com/algorithmically-generated-image-dataset-71aee957563a).

## for loops

```python
for background in ["background1", "background2", "background3"]:
    for character in ["elf1", "elf2", "elf3"]:
        for object in ["object1", "object2", "object3"]:
```

This portion of the code allows you to create you generative art. Ensure that your naming convention is consistent with the files in the folders you are referencing 

![](https://i.imgur.com/Fn5Sb3H.png)


If I want to create a custom design, or limited unique art, you can tell python to generate a specific combination or reference a specific file. 

```python
generate_image(background="background1", character="elf1", object="object1", file_name="example1")
```

## Generate

Run your main<span>.py</span> file 

```
python3 main.py
```

Your algorithmically generated image dataset will appear in "generated" folder

![](https://i.imgur.com/ZYLcotM.png)


## Hosting NFTs

https://nft.storage/

**Here is your hosted image, with a CID**
![](https://i.imgur.com/mSeqVgg.png)

Hosting NFTs on marketplaces or wallets typically request ETH and gas. NFT developers who want free decentralized storage, you will be able to host your images on-chain with NFT.storage. 

Just upload your data and you'll receive an IPFS hash of the content (a CID) that can be used in on-chain NFT data as a pointer to the content.

![](https://i.imgur.com/scEMLLd.png)


How it works:

- Upload your data, get back an IPFS hash of the content (a CID) that can be used in on-chain NFT data as a pointer.
- Storage + Retrieval is free!
- Metadata is returned in proper formats!
- Fetch it back via IPFS (pinned redundantly >3x) 
- Backed up to Filecoin (stored redundantly >5x)


[Filecoin](https://filecoin.io/) provides long term storage for the data ensuring that even if nft.storage is attacked or taken down the NFT data persists.



## Consume API
![](https://i.imgur.com/pHRQ9Zh.png)

You can upload either a single file or consume the API to upload multiple files in a directory. The API follows a typical POST and GET Method.


## Next Steps
Start building your NFTs! Join Filecoin's Hackathon and showcase your NFT projects, win prize money.

https://hackathons.filecoin.io/


## Continuing Education

## Video Tutorial

[![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/r87xutjtdij3gq7gdmsz.png)](https://youtu.be/gfkWJTBqHuE)

