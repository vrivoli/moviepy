from moviepy.editor import VideoFileClip, ColorClip
import numpy as np

# Load original video
input_path = "Indulge1.mov"  # Make sure this is in the same folder as the script
clip = VideoFileClip(input_path).subclip(0, 3)  # Adjust duration if needed

# Function to apply green to bright areas
def apply_green_background(get_frame, t):
    frame = get_frame(t)
    mask = np.mean(frame, axis=2) > 180  # Adjust threshold if needed
    new_frame = frame.copy()
    new_frame[mask] = [0, 255, 0]  # Solid green
    return new_frame

# Apply the function
processed_clip = clip.fl(apply_green_background)

# Save the result
output_path = "Indulge1_GreenEffect.mov"
processed_clip.write_videofile(output_path, codec="libx264", audio_codec="aac")
