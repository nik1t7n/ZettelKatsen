Created: 202401172219
Tags: #cs-intermediate 

---
### Reference

>[!tip] Mapping
>Mapping in programming refers to the automated process of transforming data from one structure to another. In the context of AutoMapper, it streamlines the assignment of fields and properties between objects of different types, enhancing code readability, reducing duplication, and facilitating updates to data models, commonly applied in scenarios like data transfer to views, database interactions, and integration with external APIs.

Here we are going to map data from ComputerSnake model to Computer model using **Automapper** library in C#. Let's install it:

```cs
dotnet add package Automapper
```

^84b2c2


The mapper object declaration:

```js
Mapper mapper = new(new MapperConfiguration((cfg) => {
	cfg.CreateMap<ComputerSnake, Computer>()
		  .ForMember(destination => destination.ComputerId, options =>
				options.MapFrom(source => source.computer_id));
}));
```
Here we create an instance of the Mapper. Then we create MapperConfiguration with a lambda function as an argument. Further, we are explaining to the mapper how to map our data. More precisely from where to where (ComputerSnake -> Computer). In other words we say: "Take the fields from ComputerSnake and map them to Computer by next settings". 

After we configured that destination (*ComputerId*) would be filled up from the *computer_id* field.  
And let's do it like this to all field of our models:

```js
Mapper mapper = new(new MapperConfiguration((cfg) => {
	cfg.CreateMap<ComputerSnake, Computer>()
		  .ForMember(destination => destination.ComputerId, options =>
				options.MapFrom(source => source.computer_id))
		  .ForMember(destination => destination.CPUCores, options =>
				options.MapFrom(source => source.cpu_cores))
		  .ForMember(destination => destination.HasWifi, options =>
				options.MapFrom(source => source.has_wifi))
		  .ForMember(destination => destination.HasLTE, options =>
				options.MapFrom(source => source.has_lte))
		  .ForMember(destination => destination.VideoCard, options =>
				options.MapFrom(source => source.video_card))
		  .ForMember(destination => destination.Motherboard, options =>
				options.MapFrom(source => source.motherboard))
		  .ForMember(destination => destination.ReleaseDate, options =>
				options.MapFrom(source => source.release_date))
		  .ForMember(destination => destination.Price, options =>
				options.MapFrom(source => source.price));
	}));
```

It is quite beautiful because we can correct field more detailed here. For example:
```js
.ForMember(destination => destination.Price, options =>
				options.MapFrom(source => source.price * 0.8m));
```
So, we are allowed to transform data any way we want. 

And to get a mapped result we must do:

```js
IEnumerable<Computer> computerResult = mapper.Map<IEnumerable<Computer>>(computersSystem);
```
This is instance of the Computer model but with data taken from ComputerSnake model. Cool!

- - -

However, if we want just map data from one field to another there is one easier method! Go to the file of the Model and write **\[JsonPropertyName("field")]**  above the field you want to map. 

>[!tip] **\[JsonPropertyName("field")]**
>This attribute indicates that the some property in the Computer class will be mapped to the another field when serializing/deserializing JSON using System.Text.Json. 

Code:

```cs
using System.Text.Json.Serialization;

namespace HelloWorld.Models
{
    public class Computer
		{
			[JsonPropertyName("computer_id")]
			public int ComputerId {get;set;}

			[JsonPropertyName("motherboard")]
			public string Motherboard { get; set; } = "";

			[JsonPropertyName("cpu_cores")]
			public int? CPUCores { get; set; } = 0;

			[JsonPropertyName("has_wifi")]
			public bool HasWifi { get; set; }

			[JsonPropertyName("has_lte")]
			public bool HasLTE { get; set; }

			[JsonPropertyName("release_date")]
			public DateTime? ReleaseDate { get; set; }

			[JsonPropertyName("price")]
			public decimal Price { get; set; }

			[JsonPropertyName("video_card")]
			public string VideoCard { get; set; } = "";
		}
}
```
It will do exactly the same as the previous method. The Main file code will be just:

```js
IEnumerable<Computer>? computersJsonPropertyMapping = System.Text.Json.JsonSerializer.Deserialize<IEnumerable<Computer>>(computersJson);
```
That's all! You can use it. 

---
### Zero-Links

1. 

-------
### Links

1. [[JSON]]