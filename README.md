# 2D3D_Graphics_WebGl_GlMatrix

 Nama  | NRP | Kelas
------------------- | -------------- | --------------		
Timothy Hosia Budianto | 5025211098 | Grafkom A

## SOAL
1. Make 2D square from 2 existing triangle
![image](https://github.com/thossb/2D3D_Graphics_WebGl_GlMatrix/assets/90438426/7cfb7f0d-f092-452f-984d-6cd2ff66034b)

Modified code plus documentation
```
function draw() {
    gl.clearColor(0, 0, 0, 1); // Menentukan warna yang akan digunakan untuk membersihkan canvas (hitam)
    gl.clear(gl.COLOR_BUFFER_BIT); // Membersihkan canvas (menggunakan warna yang telah ditentukan)

    /* Set up values for the "coords" attribute */

    let coords = new Float32Array([ // Membuat array Float32Array yang berisi koordinat titik-titik segitiga
    
        -0.5, -0.5,  // Koordinat titik 1 (x, y)
         0.5, -0.5,  // Koordinat titik 2 (x, y)
        -0.5,  0.5,  // Koordinat titik 3 (x, y)

         0.5, -0.5,  // Koordinat titik 4 (x, y)
        -0.5,  0.5,  // Koordinat titik 5 (x, y)
         0.5,  0.5   // Koordinat titik 6 (x, y)
    ]);

    gl.bindBuffer(gl.ARRAY_BUFFER, bufferCoords); // Mengikat buffer WebGL untuk koordinat
    gl.bufferData(gl.ARRAY_BUFFER, coords, gl.STREAM_DRAW); // Mengisi buffer dengan data koordinat segitiga
    gl.vertexAttribPointer(attributeCoords, 2, gl.FLOAT, false, 0, 0); // Mengkonfigurasi atribut vertex shader untuk menerima data koordinat
    gl.enableVertexAttribArray(attributeCoords); // Mengaktifkan atribut vertex shader untuk koordinat

    /* Set up values for the "color" attribute */

    let color = new Float32Array([ // Membuat array Float32Array yang berisi data warna segitiga
        0, 0, 1,   // Warna titik 1 (R, G, B)
        0, 1, 0,   // Warna titik 2 (R, G, B)
        1, 0, 0,   // Warna titik 3 (R, G, B)

        0, 1, 0,   // Warna titik 4 (R, G, B)
        1, 0, 0,   // Warna titik 5 (R, G, B)
        0, 0, 1    // Warna titik 6 (R, G, B)
    ]);

    gl.bindBuffer(gl.ARRAY_BUFFER, bufferColor); // Mengikat buffer WebGL untuk warna
    gl.bufferData(gl.ARRAY_BUFFER, color, gl.STREAM_DRAW); // Mengisi buffer dengan data warna segitiga
    gl.vertexAttribPointer(attributeColor, 3, gl.FLOAT, false, 0, 0); // Mengkonfigurasi atribut vertex shader untuk menerima data warna
    gl.enableVertexAttribArray(attributeColor); // Mengaktifkan atribut vertex shader untuk warna

    /* Draw the triangle. */

    gl.drawArrays(gl.TRIANGLES, 0, 6); // Menggambar segitiga menggunakan gl.TRIANGLES dengan 6 titik
}
```
  
2. Show the sides of 3D cube <br>
A 3D Cube with 1 front side open 
![image](https://github.com/thossb/2D3D_Graphics_WebGl_GlMatrix/assets/90438426/94fffca5-068e-4f32-bbbc-fd4e2f197224)

Modified code plus documentation

```
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    //drawPrimitive( gl.TRIANGLE_FAN, [0,1,0,1], [ -0.5,-0.5,-0.5, -0.5,0.3,-0.5, 0.3,0.3,-0.5, 0.3,-0.5,-0.5 ]);   //front face (dihilangkan)
    drawPrimitive( gl.TRIANGLE_FAN, [1,0,0,1], [ -0.5,0.3,0.5, -0.3,0.5,0.5, 0.5,0.5,-0.5, 0.3,0.3,-0.5 ]);         //left face
    drawPrimitive( gl.TRIANGLE_FAN, [0,0,1,1], [ 0.3,-0.5,-0.5, 0.3,0.3,-0.5, 0.5,0.5,-0.5, 0.5,-0.3,-0.5 ]);       // Top Face
    drawPrimitive( gl.TRIANGLE_FAN, [1,0.5,0,1], [ -0.5,-0.5,0.5, -0.3,-0.3,-0.5, 0.5,-0.3,-0.3, 0.3,-0.5,-0.5 ]);  // Right Face 
    drawPrimitive( gl.TRIANGLE_FAN, [1,1,0,1], [ -0.5,-0.5,0.5, -0.3,-0.3,0.5, -0.3,0.5,0.5, -0.5,0.3,0.5 ]);       // Bottom Face
    drawPrimitive( gl.TRIANGLE_FAN, [1,0,1,1], [ 0.5,-0.3,0.5, -0.3,-0.3,0.5, -0.3,0.5,0.5, 0.5,0.5,0.5 ]);         // Back Face

}
```
Explanation of the drawprimitive function
```
function drawPrimitive(primitiveType, color, vertices) {
    // Enable the attribute for vertex coordinates in the shader program.
    gl.enableVertexAttribArray(a_coords_loc);

    // Bind the vertex buffer containing the vertex data.
    gl.bindBuffer(gl.ARRAY_BUFFER, a_coords_buffer);

    // Copy the vertex data into the bound buffer as a Float32Array and specify usage as STREAM_DRAW.
    gl.bufferData(gl.ARRAY_BUFFER, new Float32Array(vertices), gl.STREAM_DRAW);

    // Set the uniform color variable in the shader program to the specified color.
    gl.uniform4fv(u_color, color);

    // Define how to interpret the vertex data in the buffer and specify its layout.
    gl.vertexAttribPointer(a_coords_loc, 3, gl.FLOAT, false, 0, 0);

    // Draw the primitive using the specified primitive type and the vertex data.
    gl.drawArrays(primitiveType, 0, vertices.length / 3);
}
```
The 3D cube after rotation (from another pov)

![image](https://github.com/thossb/2D3D_Graphics_WebGl_GlMatrix/assets/90438426/b5ce97ef-b6b1-4964-9580-9f917c8fc123)

Modified code plus documentation
```
function draw() { 
    gl.clearColor(0,0,0,1);
    gl.clear(gl.COLOR_BUFFER_BIT | gl.DEPTH_BUFFER_BIT);
    
    /* Draw the six faces of a cube, with different colors. */
    
    drawPrimitive( gl.TRIANGLE_FAN, [1,0.5,0,1], [ -0.5,-0.5,-0.5, -0.5,0.3,-0.5, 0.3,0.3,-0.5, 0.3,-0.5,-0.5 ]);     //front face
    drawPrimitive( gl.TRIANGLE_FAN, [0,1,0,1], [ -0.5,0.3,0.5, -0.3,0.5,0.5, 0.5,0.5,-0.5, 0.3,0.3,-0.5 ]);         //left face
    drawPrimitive( gl.TRIANGLE_FAN, [1,0,0,1], [ -0.5,-0.5,0.5, -0.3,-0.3,-0.5, 0.5,-0.3,-0.3, 0.3,-0.5,-0.5 ]);  // Right Face 
    drawPrimitive( gl.TRIANGLE_FAN, [0,0,1,1], [ 0.3,-0.5,-0.5, 0.3,0.3,-0.5, 0.5,0.5,-0.5, 0.5,-0.3,-0.5 ]);       // Top Face
    drawPrimitive( gl.TRIANGLE_FAN, [1,1,0,1], [ -0.5,-0.5,0.5, -0.3,-0.3,0.5, -0.3,0.5,0.5, -0.5,0.3,0.5 ]);       // Bottom Face
    drawPrimitive( gl.TRIANGLE_FAN, [1,0,1,1], [ 0.5,-0.3,0.5, -0.3,-0.3,0.5, -0.3,0.5,0.5, 0.5,0.5,0.5 ]);         // Back Face

}
```

