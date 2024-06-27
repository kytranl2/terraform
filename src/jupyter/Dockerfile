# Use the official TensorFlow GPU image as a base image
FROM tensorflow/tensorflow:2.9.0-gpu

# Set environment variables for CUDA
ENV CUDA_VERSION=11.6
ENV CUDNN_VERSION=8

# Update and install essential packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    curl \
    git \
    wget \
    python3-pip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Jupyter Notebook
RUN pip install --no-cache-dir jupyter

# Set up Jupyter Notebook
RUN jupyter notebook --generate-config && \
    echo "c.NotebookApp.ip = '*'" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.open_browser = False" >> ~/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.port = 8888" >> ~/.jupyter/jupyter_notebook_config.py

# Set the working directory
WORKDIR /workspace

# Expose the Jupyter Notebook port
EXPOSE 8888

# Define the command to run Jupyter Notebook
CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/workspace"]

# Add additional Python packages if needed (optional)
# COPY requirements.txt /tmp/
# RUN pip install --no-cache-dir -r /tmp/requirements.txt

# Copy your notebooks or scripts if needed
# COPY your_notebook.ipynb /workspace/

# Example of how to add a user (optional)
# RUN useradd -ms /bin/bash newuser && echo "newuser:newpassword" | chpasswd && adduser newuser sudo
