# CS 4331 - Project #1

## Moon House

![Main Screenshot](./ReadMeAssets/main.jpg)

### Interactions/Animations

#### Teleportation Pads

When you look at a poster on the wall or the instruction panel in the middle of the scene, you will teleport to a location close to that poster.

![Poster 1 Screenshot](./ReadMeAssets/teleporter1.JPG)
![Poster 2 Screenshot](./ReadMeAssets/teleporter2.JPG)
![Poster 3 Screenshot](./ReadMeAssets/teleporter3.JPG)
![Poster 4 Screenshot](./ReadMeAssets/teleporter4.JPG)
![Poster 5 Screenshot](./ReadMeAssets/teleporter1.JPG)
```
AFRAME.registerComponent('collider-check', {
  init: async function() {
    this.el.addEventListener("raycaster-intersected", evt => {
      this.intersectingRaycaster = evt.detail.el.components.raycaster;
      setTimeout(() => {
        if (this.intersectingRaycaster != null && sceenLoaded && !intersectedIn) {
          switch (evt.srcElement.id) {
            case "top-tp":
              movePlayer('0 0 -8')
              intersectedIn = true;
              break;
            case "left-tp":
              movePlayer('8 0 2')
              intersectedIn = true;
              break;
            case "right-tp":
              movePlayer('-8 0 0')
              intersectedIn = true;
              break;
            case "back-tp":
              movePlayer('2 0 8')
              intersectedIn = true;
              break;
            case "middle-tp":
              movePlayer('0 0 0')
              intersectedIn = true;
              break;

              ...CODE...

            default:
          }
        }
      }, 1500)
    });
  }
});

function movePlayer(position) {
  player.setAttribute("position", position);
}
```

```
<!-- (TELEPORT PADS) -->
<a-plane position="-9.962 1.699 1.832" rotation="0 90 0" class="teleporter" id="right-tp" collider-check src="./assets/images/poster1.jpg"></a-plane>
<a-plane position="9.962 1.699 1.832" rotation="0 -90 0" class="teleporter" id="left-tp" collider-check src="./assets/images/poster2.jpg"></a-plane>
<a-plane position="-4.005 1.699 -9.931" class="teleporter" id="top-tp" collider-check src="./assets/images/poster3.jpg"></a-plane>
<a-plane position="3.750 1.5 9.969" rotation="0 180 0" class="teleporter" id="back-tp" collider-check src="./assets/images/poster4.jpg"></a-plane>
```

#### Moving Truck

When you hover your cursor over the remote control in the middle of the scene it will trigger the truck to move to the right then back to its original position.

Base:
![Truck base position](car.JPG)
Active:
![Truck moving after activiation](driving.JPG)
```
AFRAME.registerComponent('collider-check', {
  init: async function() {
    this.el.addEventListener("raycaster-intersected", evt => {
      this.intersectingRaycaster = evt.detail.el.components.raycaster;
      setTimeout(() => {
        if (this.intersectingRaycaster != null && sceenLoaded && !intersectedIn) {
          switch (evt.srcElement.id) {

            ...CODE...

            case "controller":
              let car = document.querySelector('#car')
              if (!evt.srcElement.active) {
                evt.srcElement.active = true;
                car.setAttribute('animation', 'property:position; to: 4 .075 -2.569; dur: 2000; easing: linear;')
              }
              setTimeout(function() {
                car.setAttribute('animation', 'property:rotation; to: 0 270 0; dur: 2000; easing: linear;')
                setTimeout(function() {
                  car.setAttribute('animation', 'property:position; to: 1 .075 -2.569; dur: 2000; easing: linear;')
                  setTimeout(function() {
                    car.setAttribute('animation', 'property:rotation; to: 0 90 0; dur: 2000; easing: linear;')
                    evt.srcElement.active = false;
                  }, 2000)
                }, 2000)
              }, 2000)
              intersectedIn = true;
              break;

              ...CODE...

            default:
          }
        }
      }, 1500)
    });

  }
});
```

```
<!-- Model #10  CAR -->
<a-gltf-model position="1 .075 -2.569" scale=".1 .1 .1" rotation="0 90 0" src="#carD" id="car"></a-gltf-model>

<!-- Model #11  CONTROLLER -->
<a-gltf-model position="-.880 .133 -2.488" scale=".001 .001 .001" rotation="-90 0 0" src="#controller" class="controller" id="controller" collider-check active="false"></a-gltf-model>
```
#### Earth

The earth is a giant Collada model which rotates in its own axis by an a-frame animation element.

![Rotating earth](https://via.placeholder.com/150)

```
<a-entity collada-model="#planet" rotation="45 0 45" position="70 150 -100" scale="80 80 80">
	<a-animation attribute="rotation" from="45 0 45" dur="200000" to="45 360 45" repeat="indefinite" easing="linear"></a-animation>
</a-entity>
```

## Sources

### Models

11 unique models were used in building this project.

* Night Stand - https://sketchfab.com/3d-models/simple-nightstand-26d08ce396454ee3bd56ffa160e6538b
* Bed - https://sketchfab.com/3d-models/bed-403c4a48e5ea4a9fbbb9a096d90973af
* Guitar - https://sketchfab.com/3d-models/classical-guitar-ad63274604e4416a86a1175d63cadeff
* Gym - https://sketchfab.com/3d-models/gym-multiple-df5e938192244b82a1e59c7145030ee0
* Bookshelf - https://sketchfab.com/3d-models/bookshelf-b8f46cf7daca419a87ac8d131bad056f
* Plant - https://sketchfab.com/3d-models/indoor-pot-plant-3-8ad9b497549f42d4b8fa798828d6ec1e
* Truck - https://sketchfab.com/3d-models/dumptruck-qCWXrNLMlMOEtD5rcS0zOKbdkbB
* Controller - https://sketchfab.com/models/961d6215e3624c6eb861970acc953592
* Japanese Lamp - https://sketchfab.com/models/e816f01aa14b4af99a582b4d6a8cbdd0
* Window - https://sketchfab.com/models/ce64c54fc8fb443c8135ac2caa2e9243
* Box - https://sketchfab.com/models/0641e66ea33c415694cf84f786178960

### Textures

* Pizza Hut Box - https://live.staticflickr.com/1156/5149222704_75099d2392_n.jpg

### Art

* Painting 1 - https://www.etsy.com/listing/704185211/bold-and-brash-print-poster?gpla=1&gao=1&&utm_source=google&utm_medium=cpc&utm_campaign=shopping_us_ts1-c-art_and_collectibles-prints-digital_prints&utm_custom1=50c105c2-bac8-43c3-b98c-64228306159c&utm_content=go_2063581104_76452839735_367965825297_pla-328046931108_c__704185211&utm_custom2=2063581104&gclid=Cj0KCQjwqrb7BRDlARIsACwGad4Fk2wWWYSh-ry69LsPoFqbqWb43p2p7COnG4MDi7EN5Jy0tLggQaoaAvqjEALw_wcB
* Painting 2 - https://www.etsy.com/listing/711251717/my-hero-academia-poster-bakugou-katsuki?ref=pla_similar_listings_top_ad-1&plkey=bb77bac81caafa9704689595a7cb2e4704fe960b%3A711251717&frs=1
* Painting 3 - https://www.etsy.com/listing/262615370/dead-and-company-official-screen-printed?ga_order=most_relevant&ga_search_type=all&ga_view_type=gallery&ga_search_query=print+poster&ref=sc_gallery-1-19&plkey=a52ed39531ee31c86c754623d7a30a1360e28be7%3A262615370&frs=1&sca=1
* Painting 4 - http://muvial.blogspot.com/2013/01/normal-0-false-false-false-en-us-x-none.html

## References

* [A-frame](https://aframe.io/)
