mport face_recognition

# Load known face images and encode their embeddings
known_face_encodings = []
known_face_names = []

# Add known faces and their names to the lists
# For example:
# known_face_image = face_recognition.load_image_file("path/to/known_face.jpg")
# known_face_encoding = face_recognition.face_encodings(known_face_image)[0]
# known_face_encodings.append(known_face_encoding)
# known_face_names.append("John Doe")

# Load the unknown image to recognize faces
unknown_image = face_recognition.load_image_file("path/to/unknown_image.jpg")

# Find all face locations and their encodings in the unknown image
face_locations = face_recognition.face_locations(unknown_image)
face_encodings = face_recognition.face_encodings(unknown_image, face_locations)

# Iterate through detected faces and compare with known faces
for face_encoding in face_encodings:
    # Compare the face encoding with the known face encodings
    matches = face_recognition.compare_faces(known_face_encodings, face_encoding)
    name = "Unknown"  # Default name if the face is not recognized

    # Check if the face matches any known face
    if True in matches:
        first_match_index = matches.index(True)
        name = known_face_names[first_match_index]

    print(f"Found {name} in the image.")
