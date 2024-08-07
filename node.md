## Node some informaation


###  import and export files

-  import and export file Two way
1) By default follow structer (require)
   - import file and export default Key word use 
   - This type use when export Only single function
    ``` 
    const name = require("filename.js");
    modele.exports = name;
  ```  
    const {name , countAge} = require("filenmae.js");
    modele.exports = {name , countAge};
  ```
2) chnage structer  (module)
   - import file and export  
   - This type use when export Only single function
   ``` 
    import  name from "filename.js";
    export default name;
    ```  
   - This type when export multyple function

   ```
    import  {name , countAge} form require"filenmae.js";
    export {name , countAge};
    ```    


### Model in Node

```
const userSchema = new Schema(
    {
        username: {
            type: String,
            required: true,
            unique: true,
            lowercase: true,
            trim: true, 
            index: true
        },
        watchHistory: [
            {
                type: Schema.Types.ObjectId,
                ref: "Video"
            }
        ],
        password: {
            type: String,
            required: [true, 'Password is required']
        },
        views: {
            type: Number,
            default: 0
        },
          role: { type: String, enum: ['Admin', 'User'], required: true },
    },
    {
        timestamps: true
    }
)
 ```


 ### Function create in Model

 1) This function call before save new user
 ```
 userSchema.pre("save", async function (next) {
    if(!this.isModified("password")) return next();

    this.password = await bcrypt.hash(this.password, 10)
    next()
}) 
 ```

 2) Create custom function in model
 ``` 
 userSchema.methods.generateAccessToken = function(){
    return jwt.sign(
        {
            _id: this._id,
            email: this.email,
            username: this.username,
            fullName: this.fullName
        },
    )
}
 ```