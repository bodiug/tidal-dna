# Tidal DNA

Create a unique playlist with an artist-by-artist shuffle of your Tidal favorites.

---

## Description

Tidal DNA offers a fresh way to rediscover your music library. Instead of a completely random shuffle, this script creates a playlist by taking a single, random top track from each of your favorite artists. The result is a unique "artist-by-artist" shuffle that serves as a DNA sample of your musical taste.

It's fast, efficient, and a great way to listen to a broad cross-section of the artists you love without getting stuck on one album or style.

## Features

-   **Artist-by-Artist Shuffle**: Creates a playlist with one random top track per favorite artist.
-   **Concurrent Fetching**: Uses `asyncio` to fetch track information concurrently, making it very fast.
-   **Rate-Limiting**: A built-in semaphore limits concurrent API calls to avoid overwhelming the Tidal servers.
-   **Customizable Playlists**:
    -   Set a maximum number of tracks for the playlist.
    -   Specify the number of top tracks to choose from per artist.
    -   Name your playlist whatever you like.
-   **Verbose Mode**: Optional detailed output for debugging or curiosity.
-   **Safe Playlist Handling**: Clears an existing playlist only after all new tracks have been successfully fetched.

## Requirements

-   [uv](https://github.com/astral-sh/uv)

The script is self-contained and uses a shebang to declare its own Python dependencies. When you run it, `uv` will automatically create a virtual environment and install the correct version of the `tidalapi` library (`0.8.4`).

## Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/bodiug/tidal-dna.git
    cd tidal-dna
    ```

2.  **Make the script executable:**
    ```bash
    chmod +x tidal_dna.py
    ```

## Authentication

The first time you run the script, `tidalapi` will prompt you to log in. It will open a URL in your browser where you can authenticate with your Tidal account.

After a successful login, the library will save your session credentials to `~/.tidal-session-oauth.json`. On subsequent runs, the script will use this file to log in automatically.

## Usage

The script is run directly from the command line. `uv` handles the execution and dependency management automatically.

```bash
./tidal_dna.py [OPTIONS]
```

### Arguments

| Argument              | Default       | Description                                                               |
| --------------------- | ------------- | ------------------------------------------------------------------------- |
| `--session-file`      | `~/.tidal-session-oauth.json` | Path to your Tidal session file.                                          |
| `--playlist-name`     | `Tidal DNA`   | The name of the playlist to create or update.                             |
| `--tracks-per-artist` | `1`           | The number of random top tracks to select from each artist.               |
| `--max-tracks`        | (none)        | The maximum total number of tracks to include in the playlist.            |
| `-v`, `--verbose`     | (disabled)    | Enable verbose output to see detailed logs, including track-finding steps.|

---

## Examples

### Basic Usage

Create a playlist named "Tidal DNA" with one random top track from each of your favorite artists.

```bash
./tidal_dna.py
```

### Create a Smaller Playlist

Create a playlist named "My Quick Mix" with a maximum of 50 tracks.

```bash
./tidal_dna.py --playlist-name "My Quick Mix" --max-tracks 50
```

### Get More Variety

Create a playlist where each track is chosen from the top 5 tracks of each artist, instead of just the top track.

```bash
./tidal_dna.py --tracks-per-artist 5
```

### Verbose Output

Run the script with detailed logging to see every step of the process.

```bash
./tidal_dna.py --verbose
```
