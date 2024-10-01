# Docker Cleanup Script

This script is designed to clean up unused and unnecessary Docker artifacts such as stopped containers, dangling images, unused volumes, and images older than two months. It provides options for both a dry-run (for testing purposes) and production execution.

## Features
- Deletes Docker images with `<none>` as their image ID.
- Removes all stopped or dead Docker containers.
- Deletes Docker images older than two months.
- Cleans up dangling Docker images (images not associated with any containers).
- Cleans up unused Docker volumes.
- Supports dry-run mode to simulate actions without actually executing them.

## Usage

### 1. **Make the script executable:**

```bash
chmod +x docker_cleanup.sh
```

### 2. **Run the script:**

#### Dry-run mode (to simulate the process without making changes):

```bash
./docker_cleanup.sh --dry-run
```

#### Production mode (to perform actual cleanup):

```bash
./docker_cleanup.sh
```

### 3. **Script Flags:**

- **--dry-run** or **-dry-run**: Executes the script in dry-run mode where no actual deletion happens, but actions are simulated.
- **--h** or **-h**: Displays help information.

## Steps Performed

1. **Step 1:** Deletes Docker images with `ImageID` as `<none>`.
   
   If such images are found, they will be deleted unless running in dry-run mode.

2. **Step 2:** Removes all Docker containers that have `Exited` or `Dead` status.

   Only containers with these statuses are removed.

3. **Step 3:** Deletes Docker images that are older than two months.

   This helps clean up old and unused Docker images.

4. **Step 4:** Removes dangling Docker images that are no longer associated with any containers.

   These images are safe to delete, as they are not in use.

5. **Step 5:** Cleans up unused Docker volumes.

   This step removes volumes that are no longer being used by any container.

## Example

Running the script in production mode:
```bash
./docker_cleanup.sh
```

Running the script in dry-run mode:
```bash
./docker_cleanup.sh --dry-run
```

## Requirements

- **Docker**: The script expects Docker to be installed and available at `/usr/bin/docker`. You can modify the `DOCKER` variable in the script to point to your Docker binary location if needed.

## Error Handling

- If any errors occur during the deletion process, the script will log them and continue with the next steps.

## License

This script is provided under the MIT License.
