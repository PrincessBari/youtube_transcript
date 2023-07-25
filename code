from youtube_transcript_api import YouTubeTranscriptApi

def add_timestamps(transcript):
    timestamps_transcript = []
    previous_time = 0
    for entry in transcript:
        text = entry['text']
        start_time = entry['start']
        if start_time - previous_time >= 30:
            timestamp = f"[{format_time(start_time)}] "
            timestamps_transcript.append(timestamp + text)
            previous_time = start_time
        else:
            timestamps_transcript.append(text)
    return timestamps_transcript

def format_time(seconds):
    m, s = divmod(seconds, 60)
    h, m = divmod(m, 60)
    return "{:02d}:{:02d}:{:02d}".format(int(h), int(m), int(s))

def save_transcript_to_file(video_id, file_path):
    try:
        transcript = YouTubeTranscriptApi.get_transcript(video_id)
        timestamps_transcript = add_timestamps(transcript)
        with open(file_path, 'w', encoding='utf-8') as file:
            for line in timestamps_transcript:
                file.write(line + '\n')
        print(f"Transcript with timestamps saved to: {file_path}")
    except Exception as e:
        print(f"Error occurred while fetching or saving the transcript: {e}")

if __name__ == "__main__":
    video_id = 'MnkLiFV6iWo'
    output_file_path = "./output/transcript_with_timestamps.txt"
    save_transcript_to_file(video_id, output_file_path)
