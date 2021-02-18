# Minimap Package Documentation

## How to write the script

When you open up Unity, create a C# script and name it appropriately for the Minimap. After opening the script, **delete** the void Start function but change the void Update function to **void LateUpdate**. Create a public Transform variable and name it appropriately for the camera component as this will be used to **make the minimap camera follow the player**.

In the **void LateUpdate Function** write the following:

        Vector3 newPosition = [Transform variable name].position;
        newPosition.y = transform.position.y;
        transform.position = newPosition;

If you've wrote this correctly you should see the minimap camera follow the character when you test it, but it will **not rotate with the character**. If you want it to rotate with the character write the following:

        transform.rotation = Quaternion.Euler(90f, [Transform variable's name].eulerAngles.y, 0f);

You should now see the minimap camera rotating with the character. **Note that if you choose to make a public bool that determines whether the camera can rotate or not, if you turn it off, it will stay on the rotation it was set to before it was turned off.

## Components that need to be included



## Putting everything together



## Things to note

