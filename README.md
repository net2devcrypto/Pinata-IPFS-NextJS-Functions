# Pinata-IPFS-NextJS-Functions
Simple Pinata IPFS Functions for Next JS to Upload Files.


<h2> Use in your NextJS App: </h2>


Dependencies:

```shell
npm i axios
```

UPLOAD FILES TO IPFS Using PINATA:

// Replace key and secret with your Pinata api key and api secret.

FUNCTION: 


```shell

  async function sendFileToIPFS (e) {
  
        const file = e.target.files[0];
        const formData = new FormData();
        formData.append("file", file);
        
        const key = 'Your Pinata Api Key';
        const secret = 'Your Pinata Api Secret Key'
        const url = "https://api.pinata.cloud/pinning/pinFileToIPFS"
        
       
        const opts = JSON.stringify({
          cidVersion: 0,
        })
        formData.append('pinataOptions', opts);
        
        const options = {
          maxBodyLength: "Infinity",
          headers: {
          'Content-Type': `multipart/form-data; boundary=${formData._boundary}`,
            pinata_api_key: key,
            pinata_secret_api_key: secret,
            Accept: 'text/plain',
        }
      }
        const resFile = await axios.post(url, formData, options);
        const ImgHash = `ipfs://${resFile.data.IpfsHash}`;
        console.log(ImgHash);
      }
```

 Attach to your html upload button :
 
 ```shell
 
  <input
    className="btn btn-secondary"
    type="file"
    name="Asset"
    onChange={sendFileToIPFS}/>
    
 ```
 
