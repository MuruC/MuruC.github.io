---
layout: post
title: "Load Model"
date: 2021-01-10
excerpt: "Use Model class and Mesh class to load model and texture"
tags: [OpenGL, C++]
comments: true
pagetype: 3
figure: import-model.png
---

{: .center}
![image](https://user-images.githubusercontent.com/49530505/152259830-10fe4a8a-7f34-433a-9c33-168f632e694b.png "model")
{% capture images %}
{% endcapture %}

# Use Assimp library

# Mesh

I use a mesh class to store vertices, intices and texture coords.

## Set up

{% highlight c %}
    class Mesh {
       public:
           vector<Vertex> vertices;
           vector<unsigned int> indices;
           vector<Texture> textures;
           Mesh(vector<Vertex> vertices, vector<unsigned int> indices, vector<Texture> textures);
           void Draw(Shader shader);
       private:
           unsigned int VAO, VBO, EBO;
           void setupMesh();
};  
{% endhighlight %}

## Render

We get correspond uniform value name from 0 to n per texture type. like "material.texture_diffuse0", "material.texture_specular1". Give the value to active texture unit
and bind the texture.

{% highlight c %}
    class Mesh {
       public:
           vector<Vertex> vertices;
           vector<unsigned int> indices;
           vector<Texture> textures;
           Mesh(vector<Vertex> vertices, vector<unsigned int> indices, vector<Texture> textures);
           void Draw(Shader shader);
       private:
           unsigned int VAO, VBO, EBO;
           void setupMesh();
    };  
{% endhighlight %}

# Model

Use Assimp to load model and get assimp scene and assimp mesh.

We need to get data from assimp mesh to set up the mesh that we defined.

Also we need to be careful that sometimes the model does not have texture images. Instead, it has a default texture that is from the modeling software

{% highlight c %}
    unsigned int LoadTextureFromAssImp(const aiTexture* aiTex)
    {
	    if (aiTex == nullptr)
	    {
	    	return 0;
	    }
	    unsigned int textureID;
	    glGenTextures(1, &textureID);
	    glBindTexture(GL_TEXTURE_2D, textureID);

	    int width, height, nrComponents;
	    unsigned char* data = nullptr;
	    if (aiTex->mHeight == 0)
	    	data = stbi_load_from_memory(reinterpret_cast<unsigned char*>(aiTex->pcData), aiTex->mWidth, &width, &height, &nrComponents, 0);
	    else
	    	data = stbi_load_from_memory(reinterpret_cast<unsigned char*>(aiTex->pcData), aiTex->mWidth * aiTex->mHeight, &width, &height, &nrComponents, 0);
        ....
    }
{% endhighlight %}

