<template>
  <canvas  id="cvs"></canvas>
  <button @Click = "circlemet()">reset cyc</button>
  <canvas  id="line"></canvas >
  <button @Click = "linemet()">reset cyc</button>
  <canvas  id="greenbox"></canvas >
  <button @Click = "treelinemet()">reset cyc</button>
  <canvas  id="bakgcolor"></canvas >
  <button @Click = "backcolmet()">reset cyc</button>
  <p>{{ k }}</p>
  <button @Click = "num()">reset cyc</button>
</template>

<script type="module">
/* eslint-disable */
import * as WGLRTHREE from 'three/src/renderers/WebGLRenderer.js'
import * as PCTHREE from 'three/src/cameras/PerspectiveCamera.js'
import * as STHREE from 'three/src/scenes/Scene.js'
import * as BGTHREE from 'three/src/geometries/BoxGeometry.js'
import * as MBMTHREE from 'three/src/materials/MeshBasicMaterial.js'
import * as OMTHREE from 'three/src/objects/Mesh.js'
import * as CTHREE from 'three/src/math/Color.js'

export default {
    name: "Home",
    data () {
        return {
            k: 0,
            circle () {
                // 그릴 위치 정하기(id)
                var canvas = document.getElementById('cvs')
                //  몇 차원인지 확인하기
                var ctx = canvas.getContext("2d")
                // canvas 초기화
                ctx.clearRect(0, 0, canvas.width, canvas.height)
                ctx.beginPath()
                //  중심점 잡기
                var center = { x: 150, y: 70 }
                var obj = {}
                // 0도 ~ 360도 까지 10도씩 증가
                for (var i = 0; i < 360; i += 10) {
                    obj.x = Math.floor((Math.random() * 40 + 1) * Math.cos( i * (Math.PI / 180) ))
                    obj.y = Math.floor((Math.random() * 40 + 1) * Math.sin( i * (Math.PI / 180) ))
                    ctx.strokeRect( center.x+obj.x , center.y+obj.y, 0.1,0.1)
                }
            },
            line () {
                //  그려줄 위치 찾기
                var line1 = document.getElementById('line')
                //  차원 알려주기
                var ctx = line1.getContext("2d")
                ctx.clearRect(0, 0, line1.width, line1.height)
                ctx.beginPath()
                //  시작 위치 알려주기
                ctx.beginPath()
                //  0,0 시작
                ctx.moveTo(0, 0)
                //  300, 150까지 선 잇기
                ctx.lineTo(300, 150)
                //  0,0과 300,150사이 이어주기
                ctx.stroke()
            },
            treeline () {
                console.log('call treeline')
                const canvas = document.querySelector('#greenbox')
                console.log('canvas : ' + canvas)
                console.log(canvas)
                const renderer = new WGLRTHREE.WebGLRenderer(canvas)
                console.log('renderer : ' + renderer)
                console.log(renderer)
                const fov = 75
                const aspect = 2  // the canvas default
                const near = 0.1
                const far = 5
                const camera = new PCTHREE.PerspectiveCamera(fov, aspect, near, far)
                console.log('camera : ' + camera)
                console.log(camera)
                camera.position.z = 2

                const scene = new STHREE.Scene()
                console.log('scene : ' + scene)
                console.log(scene)
                const boxWidth = 1
                const boxHeight = 1
                const boxDepth = 1
                const geometry = new BGTHREE.BoxGeometry(boxWidth, boxHeight, boxDepth)
                console.log('geometry : ' + geometry)
                console.log(geometry)
                const material = new MBMTHREE.MeshBasicMaterial({color: 0x44aa88})  // greenish blue
                console.log('material : ' + material)
                console.log(material)
                const cube = new OMTHREE.Mesh(geometry, material)
                console.log('cube : ' + cube)
                console.log(cube)
                scene.add(cube)
                console.log('scene.add')

                renderer.render(scene, camera)
                console.log('renderer.render')
            },
            backcol () {
                const canvas = document.querySelector('#bakgcolor');
                const renderer = new WGLRTHREE.WebGLRenderer({canvas});
                console.log('renderer : ' + renderer)
                console.log(renderer)

                const fov = 105;
                const aspect = 2;  // the canvas default
                const near = 0.1;
                const far = 5;
                const camera = new PCTHREE.PerspectiveCamera(fov, aspect, near, far);
                console.log('camera : ' + camera)
                console.log(camera)
                camera.position.z = 2;

                const scene = new STHREE.Scene();
                console.log('scene : ' + scene)
                console.log(scene)
                scene.background = new CTHREE.Color( 0xff00ff);
                console.log('scene.background : ' + scene.background)
                console.log(scene.background)

                renderer.render(scene, camera);
                console.log(scene.background)
            }
        }
    },
    methods: {
        circlemet () {
            console.log('circle')
            this.circle()
        },
        linemet () {
            console.log('line')
            this.line()
        },
        async treelinemet () {
            console.log('treeline')
            this.treeline()
        },
        backcolmet () {
            console.log('backcol')
            this.backcol()
        },
        num () {
            this.k++
        }
    },
    beforeCreate () {
        console.log('beforeCreate')
    },
    created () {
        console.log('created')
        // this.treeline()
    },
    beforeMount () {
        console.log('beforeMount')
        // this.treeline()
    },
    mounted () {
        console.log('mounted')
        // this.treeline()
    },
    beforeUpdate () {
        console.log('beforeUpdate')
        // this.treeline()
    },
    updated () {
        console.log('updated')
        // this.treeline()
    }
};
</script>

<style>
#cvs {
    height : 200px;
    border : 1px solid black;
}
#line {
    height : 200px;
    border : 1px solid black;
}
#greenbox {
    height : 200px;
    border : 1px solid black;
}
#bakgcolor {
    height : 200px;
    border : 1px solid black;
}
</style>
