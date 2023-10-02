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
  
2. 
