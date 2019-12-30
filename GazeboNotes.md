# Gazebo Notes

## Contents
- [Using ros_control](#using-ros_control)
- [Add texture to link or 3-D model](add-texture-to-link-or-model)



## Using ros_control

Vedios:
  1. [The Construct][construct], explained all the materials quite well.

[construct]:https://www.youtube.com/watch?v=3qCh-p-hzCM
  
## Add texture to link or 3-D model
#### Creating files
To add a texture, we have to first define a material. Construct a `materials` directory containing `scripts` and `textures`.
In `textures`, save textures you planned to use in .png, .JPG or other image file format.
Then, in `scripts`, creat a `foo.material` (for example) with contant as follow:
```
  material foo/goo
{
  receive_shadows on

  technique
  {
    pass
    {
      ambient 1 1 1 1.000000
      diffuse 1 1 1 1.000000
      specular 0.03 0.03 0.03 1.000000 
      emissive 0.900000 0.900000 0.900000 1.000000

      texture_unit
      {
        texture ../textures/example.png
      }
    }
  }
}
```
where `example.png` is in `textures`

#### Add Gazebo environment parameters
In order for Gazebo to know the location of the material you created, you'll have to export `GAZEBO_RESOURCE_PATH`:
```
export GAZEBO_RESOURCE_PATH=<path-to-mterials-in-your-workspace>
```
or you can just add it in `launch` file using environmental parameter:
```
<env name="GAZEBO_RESOURCE_PATH" value="$(find amr_gazebo)/media/materials"/>
```
