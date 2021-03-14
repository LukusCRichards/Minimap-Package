# Minimap Package Documentation

## How to write the script

### MinimapCam

When you open up Unity, create a C# script and name it appropriately for the Minimap. After opening the script, **delete** the void Start function but change the void Update function to **void LateUpdate**. Create a public Transform variable and name it appropriately for the camera component as this will be used to **make the minimap camera follow the player**.

In the **void LateUpdate Function** write the following:

        Vector3 newPosition = player.position;
        newPosition.y = transform.position.y;
        transform.position = newPosition;

If you've wrote this correctly you should see the minimap camera follow the character when you test it, but it will **not rotate with the character**. If you want it to rotate with the character write the following for the upcoming **MinimapRotation** method:

        transform.rotation = Quaternion.Euler(90f, player.eulerAngles.y, 0f);

If you wrote this correctly, you should see the minimap camera rotating with the character after these next steps. **Note that if you choose to make a public bool that determines whether the camera can rotate or not, if you turn it on, it will stay on the rotation it was set to before it was turned off.

Next, create a referance to the upcoming **MinimapCamRotation** script and name it appropriately. Then create an Awake method at the top to call the function that will be used to decide whether the Minimap camera will rotate or not. Make sure it looks like this when you're done:

    MinimapCamRotation miniCamRotation;
        
    void Awake()
    {
        minimapCamRotation = GetComponent<MinimapCamRotation>();
    }

Make sure the rest of the script looks like this when you're done:

    public Transform player;
    
    void LateUpdate()
    {
        Vector3 newPosition = player.position;
        newPosition.y = transform.position.y;
        transform.position = newPosition;

        if(minimapCamRotation.miniCamCanRotate == true)
        {
            minimapCamRotation.MinimapRotation();
        }
        else
        {
            MinimapCamRotation.ReturnRotation();
        }
    }

    
### Minimap Cam Rotation

Now create another script called **MinimapCamRotation** and create a public bool called miniCamCanRotate and set its value to false. then create two **public** void functions called **Minimap Rotation** so the camera can rotate and **Return Rotation** when it's turned off so it faces north.

By now, the MinimapCamRotation script should look something like this:

    public bool miniCamCanRotate = false;
        
    public void MinimapRotation()
    {
        transform.rotation = Quaternion.Euler(90f, player.eulerAngles.y, 0f);
    }

    public void ReturnRotation()
    {
        transform.rotation = Quaternion.Euler(90f, 0f, 0f);
    }

**Remember:** What is written in the **Minimap Rotation** function is what will get the camera to rotate along with the character when it is set to do so.

## Components that need to be included

For the minimap, you need the following: A Camera, a Render Texture, a UI image and a UI Canvas.

## Putting everything together

To start off, create a new Camera GameObject for the minimap and rotate it 90 degrees on the **x axis** so it looks down at the player and change the projection from perspective to **orthographic**, then add the script that makes the minimap camera follow the player. **Make sure to change the size of the projection appropriately**.

Next, right click in the **Assets Folder** and create a Texture Renderer and name it appropriately for the minimap. This is what will make the minimap see what the camera sees. After creating the Render Texture, add the Texture Renderer to the Output Texture slot in the camera that's used for the minimap. Add a UI image to the minimap canvas, as that is what will display the visuals in the UI, and then add the same Texture Renderer to the Texture slot in the image component.

Make sure that both the **MinimapCamRotaion** and **MinimapCam** script components are attatched to the same Camera GameObject that is used for the minimap and assign the corresponding GameObjects in it.

By now, you should see what the minimap camera sees on the UI.

If you've done everything accordingly you shouldn't encounter any substantial problems.

## What to do when finished

Once you've done everything and you have not encountered any errors, you should now be able to rotate the character in the scene view and change whether the camera can 

## Things you can do to make it look better

If you want to add a 2D image that you think would give a better representation on the map, you can create another canvas and change the render mode to **World Space**. Then you can place that canvas under the world map and create another UI image and place it in that UI Canvas. Then you just need to add a 2D image to it that represent your map.

After you've done that, give the 2D map canvas a layer and name it appropriately. Then select the minimap camera and change the culling mask from everything to the layer you gave the 2D map canvas. Now you should only see the 2D image, even if it's under the map.

## Things to note

The size of your 2D image and the minimap camera matters, because if you made the map the same size as your whole large map and the minimap camera's size is small, you'll see a very large image of your 2D map and it will not be useful. **So make sure you scale everything appropriately**.

**IMPORTANT:** When referencing variable from other scripts, **always** make sure that you write an Awake method and write the variable name of the script you're refering to in it, because if you don't, **it will not work**.
