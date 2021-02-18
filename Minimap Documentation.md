# Minimap Package Documentation

## How to write the script

When you open up Unity, create a C# script and name it appropriately for the Minimap. After opening the script, **delete** the void Start function but change the void Update function to **void LateUpdate**. Create a public Transform variable and name it appropriately for the camera component as this will be used to **make the minimap camera follow the player**.

In the **void LateUpdate Function** write the following:

        Vector3 newPosition = [Transform variable name].position;
        newPosition.y = transform.position.y;
        transform.position = newPosition;

If you've wrote this correctly you should see the minimap camera follow the character when you test it, but it will **not rotate with the character**. If you want it to rotate with the character write the following:

        transform.rotation = Quaternion.Euler(90f, [Transform variable's name].eulerAngles.y, 0f);

If you wrote this correctly, you should see the minimap camera rotating with the character. **Note that if you choose to make a public bool that determines whether the camera can rotate or not, if you turn it on, it will stay on the rotation it was set to before it was turned off.

If you want the minimap camera ro return to its position it was set to when it starts turned off, organise it in this (or similar) fashion:

    public bool miniCamCanRotate = false;

    public Transform player;

    // Update is called once per frame
    void LateUpdate()
    {
        Vector3 newPosition = player.position;
        newPosition.y = transform.position.y;
        transform.position = newPosition;

        if(miniCamCanRotate == true)
        {
            MinimapRotation();
        }
        else
        {
            ReturnRotation();
        }
    }

    public void MinimapRotation()
    {
        transform.rotation = Quaternion.Euler(90f, player.eulerAngles.y, 0f);
    }

    public void ReturnRotation()
    {
        transform.rotation = Quaternion.Euler(90f, 0f, 0f);
    }

## Components that need to be included

For the minimap, you need the following: A Camera, a Render Texture, a UI image and a UI Canvas.

## Putting everything together

To start off, create a new Camera GameObject for the minimap and rotate it 90 degrees on the **x axis** so it looks down at the player and change the projection from perspective to **orthographic**, then add the script that makes the camera follow the player. **Make sure to change the size of the projection appropriately**.

Next, right click in the **Assets Folder** and create a Texture Renderer and name it appropriately for the minimap. This is what will make the minimap see what the camera sees. After creating the Render Texture, add the Texture Renderer to the Output Texture slot in the camera that's used for the minimap. Add a UI image to the minimap canvas, as that is what will display the visuals in the UI, and then add the same Texture Renderer to the Texture slot in the image component.

By now, you should see what the minimap camera sees on the UI.

If you've done everything accordingly you shouldn't encounter any substantial problems.

## Things you can do to make it look better

If you want to add a 2D image that you think would give a better representation on the map, you can create another canvas and change the render mode to **World Space**. Then you can place that canvas under the world map and create another UI image and place it in that UI Canvas. Then you just need to add a 2D image to it that represent your map.

After you've done that, give the 2D map canvas a layer and name it appropriately. Then select the minimap camera and change the culling mask from everything to the layer you gave the 2D map canvas. Now you should only see the 2D image, even if it's under the map.

## Things to note

